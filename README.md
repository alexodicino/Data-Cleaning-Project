# Data Cleaning Project
## Original Dataset
General Directory of Political and Social Investigations, 1920-1952
https://www.estudioshistoricos.inah.gob.mx/guia/indicetematico.html
> Instituto Nacional de Antropología e Historia: Dirección de Publicaciones de la Coordinación Nacional de Difusión. (2006). Dirección General de Investigaciones Políticas y Sociales, 1920-1952. Guía Del Fondo de La Secretaria de Gobernación. Retrieved from https://www.estudioshistoricos.inah.gob.mx/guia/indicetematico.html

-----------------------------------------------------------------------------------------------------------------------------------------
## Description
This dataset comprises the records of the Mexican National Institute for Anthropology and History. Specifically, their records from the Division of Social and Political Investigations, 1920-1952. The dataset consists of 18,425 entries, each relating to persons or groups of interest, informants, or clandestine operatives that were being monitored by the Mexican Confidential Department (their principle intelligence organization during the period). The dataset has been used for some historical research to date and has shown value for research concerning all of North America. Consequently, it has been cleaned pursuant to the needs of researchers with limited to advanced proficiency in Spanish. Furthermore, the dateset has been cleaned and augmented to make it more conducive to visualization with tools such as TimeMapper (http://timemapper.okfnlabs.org) and TimelineJS (http://timeline.knightlab.com). All of these transformations were conducted under the assumption that future unique contributions to historical knowledge will require analyzing data in greater quantity and in multiple facets in tandem.
## Problems with the Dataset
The dataset showed signs of manual transcription into the final XML file. Consequently, there were some inconsistencies in date format, place format, department format, and subject format. Additionally, OpenRefine was unable to process dates written in Spanish, even when running OpenRefine itself in Spanish. In that state, OpenRefine could not transform the cell contents to date values in bulk.
## Transformations by Column
### Numero
The first column of the original dataset was named "Numero" (trans. "Number"). It was a simple number sequence attached to each row. As OpenRefine attached numbers to each of the rows when the dataset was imported, this column was deleted.
### Fecha inicio/Fecha término
The second and third columns were named "Fecha inicio" (trans. "date begin") and "Fecha término" (trans. "date end") respectively. The columns were first translated into English as "DateStatrt" and "DateEnd". Because OpenRefine did not understand Spanish month names, each column was faceted by text. Month names were then clustered and translated to English. Many of the cells in these columns still contained whitespace which prevented OpenRefine from understanding the Month/Year format. Leading and trailing white space was trimmed from all cells in each column. This allowed the "transform to date" function to run properly, transforming the values in each cell to numeric Year-Month-Day format. Fifty-nine cells labeled "S/F" (Sin Fecha, trans. "without date") remained. These were left unchanged.
### Lugar
The fourth column was named "Lugar" (Lit. "Place") and renamed to "Place". This cell values in this column were meant to indicate the coverage of each entry by state or country (if outside Mexico). Locations were separated by commas and cells with two or more locations also included an "y" (Lit. "and"). This column was faceted by text in order to isolate the occurrence of each word and place name. "Y" was subsequently removed from each string and replaced with a comma, leaving just the comma separated place names. Then, as Mexico consists of thirty-two states and only two other countries were mentioned (the United States and Canada), I deemed it reasonable to apply preferred place names as dictated by the Getty Thesaurus of Geographic Names. This meant updating certain place names such as "Distrito Federal" (trans. "Federal District") to thier current proper names. In the case of the Federal District, which has since been disolved, it meant transforming all occurences to "Ciudad de México" (trans. "Mexico City).
### Oficina de Información Política y Social
This column (trans. Office of Political and Social Information) specified the government office that created each entry. Text faceting showed that only seven distinct government offices were cited. The name of each office was translated into English and applied in bulk through the text facet cell.
### Tema
This column involved the most labor intensive transformations. Translating literally as "topic", this column was renamed to "Subject". Though it contained roughly six hundred unique subject headings, it seemed particularly important to translate and rectify any inconsistencies in these headings as they would be necessary for researchers. Text faceting and clustering showed small typos and punctuation discrepancies between certain subject headings. Correcting and combining the respective headings, brought the total down to five hundred and tend unique subject headings. There were some subject headings which were nearly identical to others, but with the addition of a word or two. These were not combined as they most likely were not simple transcription errors and likely reflected the original cataloging. The remaining five hundred and ten subject headings were translated into English and applied to the relevant rows.
### Asunto
"Asuntos" can refer to "affairs", "bussiness", "matters", etc. For clarity, this column was named "description". As each entry is unique and, in some cases, lengthy, these entries were not translated. Date, place, and subject values should be sufficient to narrow searches and make it reasoble to utilize a translation tool for the remaining description entries.
### Observaciones
All of the values in this column (lit. "observations") were unique. Not all rows held any values in this column, but two-thousand and forty of them did, making individual translation unreasonable.
## Unsuccessful Transformations
I attempted to get OpenRefine to combine the DateStart and DateEnd columns, and assign a timespan value between adjacent cells, but was unsuccessful in writing a GREL script that would accomplish this.
