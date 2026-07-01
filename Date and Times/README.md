# Date and Times

An analyzer for dates and times

## Analyzer Notes

This is an NLP++ Analyzer that parses through text and identifies date and time expressions written in a wide variety of formats. Some sample dates and times can be found in input/test.txt

The analyzer recognizes many common ways of writing dates and times, including:

- Numeric dates: `02/05/2020`, `06-17-2014`, `11. 12. 2014`
- Month-name dates: `December 10, 2014`, `Sept 04, 2014`, `31 Oct 2021`
- Ordinal-day dates: `19th day of May, 2015`, `july 3rd 2013`, `September 2nd, 1998`
- Weekday-prefixed dates: `Fri, 12 Dec 2014`, `Wed Aug 05 12:00:00 EDT 2015`
- Standalone years: `2004`
- Times: `10:04am`, `2:21 p.m.`, `10:04:23 pm`
- Zulu / ISO 8601 timestamps: `2017-02-03T09:04:08Z`, `2016-02-04T20:16:26+00:00`

For each date or time identified in the text, the analyzer extracts the individual fields it can determine, which may include:

- day of the month
- month
- year
- weekday name
- hour, minute, and second
- am/pm marker
- zulu (UTC offset) information for ISO 8601 timestamps

The recognized dates and times are highlighted in the final output.

To run the analyzer, create a text file in the input folder consisting of the text to be parsed.
