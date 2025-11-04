# poke-stats
Analysis of the stats for all 1025 Pokemon species and variants in Python for my final project

https://drive.google.com/file/d/1tVBRw3QfR3HeZ_NLM_XZbFcI826Qyyk0/view?usp=sharing

<b>Purpose:</b>
I am looking to analyze Pokemon statistics (stats) across generations to see if there is any sort of power-creep when comparing newer vs older Generations of Pokemon.

<b>Data Cleaning:</b>
The data was already clean upon intake, which I checked by checking the Pokemon database (Bulbapedia) for the total of unique species in the Pokedex. The total was 1025 unique species, not counting alternate forms (alt_forms).

Upon filtering alt_forms into their own set, the total of remaining species in base_forms was left at 1025, with none of them having null values save for the expected nulls in the "Secondary Typing" category.

There was one small issue of Generation grouping in the wrong order due to the original dataset showing generation numbers in Roman numerals instead of Arabic numerals. Using df.replace() was a simple matter of ensuring the Generation column would group correctly for the line chart.

<b>Data Manipulation:</b>
Firstly, having filtered the forms into the alt_forms and base_forms DataFrames, I then made two more filtered DataFrames: one for monotypes (Pokemon who lack a Secondary Typing category) and one for dual_types (Pokemon with a Secondary Typing), both done by filtering for the boolean variable in Secondary Typing Flag helpfully provided by the dataset's author.

Nextly, I grouped by Generation, looking at the means of their stat totals and individual stats. I also grouped by Legendary Status out of curiosity of how different the stats looked like across the board comparing base Pokemon vs Legendary Pokemon.

<b>Data Visualization and Statistical Analysis:</b>
My first visual was a JointPlot to show the distributions of Catch Rate in combination with Base Stat Total. A brief explanation on Catch Rate: Higher catch rates mean that the Pokémon is easier to catch, up to a maximum of 255.
<img width="594" height="590" alt="download" src="https://github.com/user-attachments/assets/2d6e295e-b6e5-41b7-bc90-8c2a5a69e372" />

With this in mind, an interesting picture takes shape almost immediately with a right-skewed distribution of Catch Rate. This implies that, given a random Pokemon, the chances of catching them are not in favor of being caught on the first try.

However, the distribution of the Base Stat Total has a far more regular distribution, with only a very small right-skew. Visual observation alone seems to suggest odds that, again given a random Pokemon, a Pokemon will favor having weaker stats only slightly over having stronger ones.

Overall the correlation between Catch Rates and Base Stat Total does seem to have a moderate-strong negative correlation, with the code showing a .corr() of -0.697 between those two variables.

Next, I passed the Generation DataFrame that's grouped by stat averages (gen_avg) into a LinePlot. In so doing, an interesting story appeared with the first two generations being the lowest in stat averages, with the Third and Fourth Generations rising higher before each Generation began to ping pong up and down, trending upwards.

<img width="571" height="455" alt="download" src="https://github.com/user-attachments/assets/47574522-2fe0-4e71-8fcc-74af5a4c7b71" />

Finally, I wished to know how the distribution of how many evolution stages (Number of Evolution) a given Pokemon would have. Across the entire dataset, a slightly unexpected result made itself known upon plotting it out on a Histogram. The greatest distribution is heavily in favor of 2-stage evolution lines, with that maximum coming in at a whopping 45%! Right behind that is 3-stage evolution lines with 33% of entries, while single-stage species make up only 22%. But interestingly enough, while 2-stage evolution lines are singularly more numerous than either 3-stage or 1-stage lines, the combination of 1-stage and 3-stage lines together outstrip 2-stage lines.
<img width="571" height="455" alt="download" src="https://github.com/user-attachments/assets/0eb6e58d-9f76-4b60-85c7-8a4cff1acfd6" />

<b>Conclusion:</b>
Overall, it does appear to me that my initial thought that "Generational Power Creep" is occurring. It began in Generation III (the generation notable for one of my favorite evo-lines, Blaziken) and ping-ponged up and down with each pair of up-down being higher than the last. In terms of catching Pokemon for competitive battling, it should be also noted that the higher a Pokemon's Base Stat Total, the harder it will be to catch them.
