/*
Title: Countdown
*/

You can use the countdown variable to create commands that display the time left until a specified date. For example, you may want to countdown until a special event on stream, or until when the stream will start every day.

## Usage

The countdown variable accepts two kinds of arguments: a **date/time** or a **time**

### Date/Time

> $(countdown `date/time`)

`date/time` is the specific date/time you wish to count down to

It can accept variants of dates, but it works best with dates in the format: `Month Day Year HH/MM/SS AM/PM TZ`

#### Example Usage

> $(countdown Dec 25 2015 12:00:00 AM EST)

will result with a response in this format

> 1 day, 3 hours, 20 minutes, 30 seconds

### Time

> $(countdown `time`)

`time` is the specific time you wish to count down to (the countdown resets daily)

It can accept variants of dates, but you will find it works best with dates in the format: `HH/MM/SS AM/PM TZ`

#### Example Usage

> $(countdown 5:00:00 PM EST)

will result with a response in this format

> 3 hours, 20 minutes, 30 seconds


## Examples

#### Adding a command to show chatters when your special Christmas stream begins

> !commands add !christmas Christmas Countdown: $(countdown Dec 25 2015 12:00:00 AM EST)


#### Adding a command to show chatters when your stream starts daily

> !commands add !starting The stream is starting in $(countdown 5:00:00 PM EST)
