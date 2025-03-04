# Dates and Times

Expressing dates and times in a clear and unambiguous way helps support people with varying backgrounds and reduces confusion.

## Dates

Different parts of the world put parts of the date in a different order for numeric dates. For example, the date "04/05/09" can mean:

- May 4th, 2009 in the United Kingdom where the order is usually day, month, then year.
- April 5th, 2009 in the United States where the order is usually month, day, then year.
- May 9th, 2004 in China where the order is usually year, month, then day.

For this reason, we should prefer using words to express dates. However, if you need to use a numeric date, then refer to the [Numeric dates](#numeric-dates) section.

### Written Dates

In general, spell out the names of months and days of the week in full. Give the full four-digit year, not a two-digit abbreviation. Also, don't use ordinal numbers such as 1st, 12th, or 23rd, for days.

This doesn't mean that you should never use ordinal numbers. There are times where including ordinals will improve the readability of text. A good rule of thumb is:

- **Omit ordinals** when the date is formatted conventionally (e.g., "January 7, 2025" or "March 3").
- **Use ordinals** when the date is written in a way that resembles spoken language (e.g., "the 7th day of the 1st month").

#### Comma Placement

Please refer to the below table for comma placement. I will point out that the `MONTH YEAR` format doesn't have a comma. This in contrast to:

- `MONTH DAY, YEAR`, 
- `QUARTER, YEAR`
- `WEEK_OF_YEAR, YEAR`

The reason for this is those dates follow a "`TERM NUMBER, YEAR`" format. However, "`MONTH YEAR`" follows a `TERM NUMBER` format. This is why there's no comma being used.

| Format                                                 | Example                                       | Example with abbreviations |
| ------------------------------------------------------ | --------------------------------------------- | -------------------------- |
| `QUARTER, WEEK_OF_YEAR, DAY_OF_WEEK, MONTH, DAY, YEAR` | Quarter 1, Week 3, Thursday, January 19, 2024 | Q1, W3, Thu, Jan 19, 2024  |
| `WEEK_OF_YEAR, DAY_OF_WEEK, MONTH, DAY, YEAR`          | Week 3, Thursday, January 19, 2024            | W3, Thu, Jan 19, 2024      |
| `DAY_OF_WEEK, MONTH DAY, YEAR`                         | Thursday, January 19, 2017                    | Thu, Jan 19, 2024          |
| `MONTH DAY, YEAR`                                      | January 19, 2017                              | Jan 19, 2017               |
| `QUARTER, YEAR`                                        | Quarter 3, 2024                               | Q3, 2024                   |
| `WEEK_OF_YEAR, YEAR`                                   | Week 3, 2017                                  | W3, 2017                   |
| `MONTH YEAR`                                           | January 2017                                  | Jan 2017                   |

#### Abbreviations

In most cases, we should defer to using the full versions of dates. However, in situations where not a lot of space is available, then it is okay to use abbreviations. If you do use an abbreviation, then make sure you use abbreviations through the entire date. Be consistent in where you apply abbreviations. For example, if you choose to abbreviate in table cells, then use abbreviations in all table cells.

The rule of thumb is to progressively go to smaller abbreviations. Start with the full word, then three-letter, two-letter, and one-letter as the UI space does not permit the larger variants.

Abbreviations should be written in sentence case (Feb), not all uppercase (FEB).

Lastly, don't end abbreviations with a period.

##### Day of week

| Full term | Three-letter abbreviation | Two-letter abbreviation | One-letter abbreviation |
| --------- | ------------------------- | ----------------------- | ----------------------- |
| Sunday    | Sun                       | Su                      | S                       |
| Monday    | Mon                       | Mo                      | M                       |
| Tuesday   | Tue                       | Tu                      | T                       |
| Wednesday | Wed                       | We                      | W                       |
| Thursday  | Thu                       | Th                      | T                       |
| Friday    | Fri                       | Fr                      | F                       |
| Saturday  | Sat                       | Sa                      | S                       |

##### Week of Year

| Full term | Abbreviation |
| --------- | ------------ |
| Week 1    | W1           |

##### Months

| Full term | Three-letter abbreviation | Two-letter abbreviation | One-letter abbreviation |
| --------- | ------------------------- | ----------------------- | ----------------------- |
| January   | Jan                       | Ja                      | J                       |
| February  | Feb                       | Fe                      | F                       |
| March     | Mar                       | Mr                      | M                       |
| April     | Apr                       | Ap                      | A                       |
| May       | May                       | My                      | M                       |
| June      | Jun                       | Jn                      | J                       |
| July      | Jul                       | Jl                      | J                       |
| August    | Aug                       | Au                      | A                       |
| September | Sep                       | Se                      | S                       |
| October   | Oct                       | Oc                      | O                       |
| November  | Nov                       | Nv                      | N                       |
| December  | Dec                       | De                      | D                       |

##### Quarter

| Full term | Abbreviation |
| --------- | ------------ |
| Quarter 1 | Q1           |

### Numeric dates

If you need to use a numeric date, then use the format `YYYY-MM-DD`, and separate the numbers using hyphens. This conforms to [ISO 8601 international standards](https://wikipedia.org/wiki/ISO_8601) for numerical date format.

### Dates with times

If you need to have a date with a time, write the date first and then the time. For example:

- 2017-04-15 at 3 PM
- May 4, 2009, at 6 PM

## Times

In general, use the following guidelines to format times:

- Use the 12-hour clock, except if required to use a 24-hour time, such as when documenting features that use 24-hour time. If the UI, a command, or a code sample uses the 24-hour format, use that format throughout the page for consistency.
- Use exact times when possible, but noon and midnight are OK.
- Use hyphens in time ranges. Don't add spaces before or after the hyphens. For example, "5-10 minutes ago".
- Capitalize AM and PM, and leave one space between it and the time. For example, "3:45 PM".
- Remove the minutes from round hours. For example, "3:00 PM" becomes "3 PM".

### Abbreviations

We should defer to using the full versions of times. However, when space is limited, it is okay to use abbreviations. The rules for time abbreviations are:

- If you use an abbreviation, then be consistent with its usage.
- Use abbreviations when space is limited and the larger versions do not fit.
- Use all lowercase letters. This is different from how we handle date casing.

| Unit            | Abbreviation |
| --------------- | ------------ |
| day, days       | d            |
| hour, hours     | h            |
| minute, minutes | min          |
| month, months   | mo           |
| second, seconds | sec          |
| week, weeks     | wk           |
| year, years     | yr           |
