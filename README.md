# SwiftUIDatePickerDialog

**Fully-customizable SwiftUI date/time picker dialog**. Features include:

* Optional dialog title.
* Selected date binding.
* Choose which picker component to display - date, time or both.
* Supports all SwiftUI `DatePicker` styles - default, compact, wheel and graphical.
* Specify valid range of selectable dates.
* Fully cancellable - cancelation reverts date selection to the original value, from when the dialog was first displayed.
* Set dialog background color.
* Dialog-wide foreground color, affecting the title, date picker and buttons.
* Fully customizable buttons - any number, any content, any action - with default confirmation and cancellation buttons.

Examples of the dialog in action:

* Graphical-style:

![Graphical dialog](https://github.com/globulus/swiftui-date-picker-dialog/blob/main/Images/graphical-green-pink.png?raw=true)

* Compact-style (default):

![Compact dialog](https://github.com/globulus/swiftui-date-picker-dialog/blob/main/Images/compact-red-purple.png?raw=true)

* Wheel dialog:

![Wheel dialog](https://github.com/globulus/swiftui-date-picker-dialog/blob/main/Images/wheel-orange-blue.png?raw=true)

* Dialog with custom buttons:

![Custom button dialog](https://github.com/globulus/swiftui-date-picker-dialog/blob/main/Images/custom-button.png?raw=true)

## Installation

This component is distributed as a **Swift package**.

## Sample usage

Use the `dateTimePickerDialog` modifier on the View on top of which you want to display the dialog:

```swift
struct DateTimePickerDialogTest: View {
    @State private var isShowing = true
    @State private var date = Date()
    let style: DateTimePickerDialog.Style
    let displayComponents: DatePickerComponents
    private let backgroundColor = Color.blue.opacity(0.1)
    private let textColor = Color.orange
    
    var body: some View {
        List(1..<6) {
            Text("\($0)")
                .onTapGesture {
                    self.isShowing = true
                }
        }.dateTimePickerDialog(isShowing: $isShowing,
                               cancelOnTapOutside: true,
                               selection: $date,
                               displayComponents: displayComponents,
                               style: style,
                               backgroundColor: backgroundColor,
                               foregroundColor: textColor,
                               buttons: [
                                .default(label: "Default"),
                                .cancel(label: "Cancel"),
                                .custom(label: { Text("Call mom").foregroundColor(.red) }, action: { dialog in
                                    
                                })
                               ]) {
            Text("Custom label")
        }
    }
}

struct DateTimePickerDialogWheel_Previews: PreviewProvider {
    static var previews: some View {
        DateTimePickerDialogTest(style: .wheel, displayComponents: [.date, .hourAndMinute])
    }
}

@available(iOS 14.0, *)
struct DateTimePickerDialogCompact_Previews: PreviewProvider {
    static var previews: some View {
        DateTimePickerDialogTest(style: .compact, displayComponents: [.date])
    }
}
```
