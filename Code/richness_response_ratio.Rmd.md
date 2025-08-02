# Richness Response Ratio Analysis (Recreate Paper Figure)
library(ggplot2)
library(dplyr)

# Classify treatments based on watershed names
final_data <- final_data %>%
  mutate(treatment_type = case_when(
    str_starts(Watershed, "N") ~ "Bison",
    str_starts(Watershed, "C") ~ "Cattle", 
    TRUE ~ "Ungrazed"
  ))

# Calculate yearly averages by treatment
yearly_richness <- final_data %>%
  group_by(RecYear, treatment_type) %>%
  summarise(mean_richness = mean(richness, na.rm = TRUE), .groups = 'drop') %>%
  pivot_wider(names_from = treatment_type, 
              values_from = mean_richness,
              names_prefix = "richness_")

# Calculate response ratios (ln(treated/ungrazed))
yearly_response <- yearly_richness %>%
  mutate(
    bison_response = log(richness_Bison / richness_Ungrazed),
    cattle_response = log(richness_Cattle / richness_Ungrazed)
  ) %>%
  select(RecYear, bison_response, cattle_response) %>%
  pivot_longer(cols = c(bison_response, cattle_response),
               names_to = "treatment", 
               values_to = "response_ratio") %>%
  mutate(treatment = case_when(
    treatment == "bison_response" ~ "Bison",
    treatment == "cattle_response" ~ "Cattle"
  ))

# Plot response ratios over time
ggplot(yearly_response, aes(x = RecYear, y = response_ratio, color = treatment)) +
  geom_line(size = 1.2) +
  geom_point(size = 2) +
  scale_color_manual(values = c("Bison" = "red", "Cattle" = "blue")) +
  labs(x = "Year", 
       y = "Native species\nRichness Response (ln[Rg/Ru])",
       title = "Richness Response to Grazing Over Time",
       color = "Treatment") +
  theme_minimal() +
  theme(legend.position = "top")

# Optional: Add reference lines if you have global data
# geom_hline(yintercept = 0.5, linetype = "dashed", alpha = 0.7) +  # 95th percentile
# geom_hline(yintercept = 0.0, linetype = "solid", alpha = 0.7)      # 50th percentile