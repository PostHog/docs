Trends are a very powerful way to visualize how actions are varying over time.

These are useful for monitoring which parts of your products are being used repeatedly.

You can watch our short Trends training videos here:

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/q39B-QAFZUI/0.jpg)](http://www.youtube.com/watch?v=q39B-QAFZUI)
[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/8IsCrLOpRCw/0.jpg)](http://www.youtube.com/watch?v=8IsCrLOpRCw) 

## Viewing action trends

Go to ’Trends’ in the left hand navigation:

![Left hand navigation - trends highlighted](https://posthog.com/wp-content/uploads/2020/03/Posthog.png)

Select the actions you want to see trends of in the menu

![Trends, action selection](https://posthog.com/wp-content/uploads/2020/03/Posthog-1.png)

You can now see the trend in these actions over time.

![Action trends](https://posthog.com/wp-content/uploads/2020/03/Posthog-2.png)

## Trend filtering

There are a few ways to filter this information.

Firstly, if you have many actions defined, you can just select a handful at a time by using the filters on the right hand side.

You can also filter this data by time, and you can display it as a table or as a line chart:

![Trend filtering](https://posthog.com/wp-content/uploads/2020/02/Screenshot-2020-02-09-at-17.30.22.png)

## Trend segmentation

It is possible to segment the data using the ‘Breakdown by’ menu. This allows you to see how trends in Actions vary by the Event properties.

This segmentation has many use cases.

For example, one of the Event properties is the UTM tags – which allows you as a marketer to understand exactly how different ad campaigns are performing.

Another example is that as a product-person, you can see if different devices or different browsers affect usage. Maybe people using your web-based application on mobiles are generally inactive because the interface is hard to use:

![Trend segmentation](https://posthog.com/wp-content/uploads/2020/02/Screenshot-2020-02-09-at-17.31.36.png)

You can filter the event data too, based on the Event property. This means instead of breaking out more lines or rows in the table, you can just display the exact Action trends you care about when the Event property is something specific.

You can also use this at the same time as the ‘Breakdown by’ option.

### Trend segmentation by Event property

For example, if you ran a movie streaming service, you could monitor ‘Play button – clicked’ for just one movie at a particular URL:

![trend segmentation by event property](https://posthog.com/wp-content/uploads/2020/02/Screenshot-2020-02-09-at-17.35.24.png)

### Trend segmentation by Stickiness

Trend graphs will show numbers by volume as default, it is possible to show this as stickiness. Instead of the total number of times this action had been completed it will chart the graph as the number of consecutive days a unique user has performed that action. This will allow you to optimize for repeatable actions. 

To do this select 'Shown As'

![stickiness](https://posthog.com/wp-content/uploads/2020/03/Posthog-6.png)

And the graph will convert to Stickiness.

![stickiness image 2](https://posthog.com/wp-content/uploads/2020/03/Posthog-7.png)


