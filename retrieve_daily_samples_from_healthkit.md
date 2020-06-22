https://stackoverflow.com/questions/13324633/nsdate-beginning-of-day-and-end-of-day

**Swift 4**

`Date` extension with (computed) properties for start/end of day/month.

```swift
extension Date {
    var startOfDay: Date {
        return Calendar.current.startOfDay(for: self)
    }

    var endOfDay: Date {
        var components = DateComponents()
        components.day = 1
        components.second = -1
        return Calendar.current.date(byAdding: components, to: startOfDay)!
    }

    var startOfMonth: Date {
        let components = Calendar.current.dateComponents([.year, .month], from: startOfDay)
        return Calendar.current.date(from: components)!
    }

    var endOfMonth: Date {
        var components = DateComponents()
        components.month = 1
        components.second = -1
        return Calendar.current.date(byAdding: components, to: startOfMonth)!
    }
}
```

Use the `Date` extension to create a HealthKit querty with the day bounds as parameters.

```
let predicate = HKQuery.predicateForSamples(withStart: now.startOfDay, end: now.endOfDay)
```

**Swift 5**

```swift
let date = Date() // current date or replace with a specific date
let calendar = Calendar.current
let startTime = calendar.startOfDay(for: date)
let endTime = calendar.date(bySettingHour: 23, minute: 59, second: 59, of: date)
```
