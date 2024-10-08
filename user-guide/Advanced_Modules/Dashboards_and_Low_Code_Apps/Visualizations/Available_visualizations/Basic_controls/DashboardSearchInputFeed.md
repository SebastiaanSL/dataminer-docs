---
uid: DashboardSearchInputFeed
---

# Search input

Available from DataMiner 10.3.0 [CU16]/10.4.0 [CU4]/10.4.7 onwards<!--  RN 39555 -->. This basic control allows users to enter text that will then be available as a string feed in the dashboard or low-code app. The string feed can be used by queries and by script parameters in low-code app actions. This string feed can also be cleared with an "x" button available in the input.

You can drag a data feed to the component to link it to that feed, or [specify a feed in the URL](xref:Specifying_data_input_in_a_dashboard_URL). This way, the component will be filled in based on the feed, but users will still be able to modify the value.

The following options are available to fine-tune the component layout:

- *Label*: Text that will be displayed next to the text input box.

- *Inline*: Determines whether the label is displayed above the text input box or next to it. If this option is selected, it is displayed next to the box.

- *Placeholder*: Placeholder that will be displayed inside the text input box.

- *Icon*: Icon that will be displayed in the text input box.

In the *Settings* tab, you can also configure the following optional settings:

- *Feed value on*: Determines when the value in the box becomes available as a feed. This can be when the user presses Enter ("Enter"), when the focus is no longer on the box ("Focus lost"), or when the value in the box changes ("Value change"). If you select *Focus lost*, the value will also become available when the user presses Enter.

## Component actions

From DataMiner 10.3.0 [CU18]/10.4.0 [CU6]/10.4.9 onwards<!--RN 40252-->, when you have added a search input component to a low-code app, you can configure the following [component action](xref:LowCodeApps_event_config#executing-a-component-action) in your low-code app to interact with the component:

- *Set value*: Allows you to set the current value of the component to either a static value or a feed.

  > [!NOTE]
  > When the component has the *General > Feed value on > Value change* option enabled, the value will immediately be passed as the component's feed. If this option is not enabled, the value will only be passed when Enter is pressed (if the *General > Feed value on > Enter* option is enabled) or when the focus is no longer on the box (if the *General > Feed value on > Focus lost* option is enabled).
