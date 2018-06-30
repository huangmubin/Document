# User Notifications (本地通知、本地推送)

https://developer.apple.com/documentation/usernotifications/unusernotificationcenter#relationships

使用 UNUserNotificationCenter 对象管理应用程序或扩展中所有与通知相关的行为。

* 通知权限
* 通知类型
* 本地推送
* 远程推送服务 APNs
* 管理已送达的通知
* 处理通知和通知相关操作
* 管理设置和授权

##  请求使用通知权限

Asking Permission to Use Notifications

https://developer.apple.com/documentation/usernotifications/asking_permission_to_use_notifications

用于本地和远程推送通知。

### 1. 请求授权

```
// 请求授权显示警报和播放声音
// 应用程序首次发出此授权请求时, 系统会提示用户授予或拒绝请求并记录用户的响应。随后的授权请求不会提示用户。

let center = UNUserNotificationCenter.current()
// Request permission to display alerts and play sounds.
center.requestAuthorization(options: [.alert, .sound]) 
   { (granted, error) in
      // Enable or disable features based on authorization.
   }
```

### 2. 检查应用的授权设置

```
// 检查应用的授权设置

let notificationCenter = UNUserNotificationCenter.current()
        
notificationCenter.getNotificationSettings { (settings) in
   // Do not schedule notifications if not authorized.
   guard settings.authorizationStatus == .authorized else {return}

   if settings.alertSetting == .enabled {         
      // Schedule an alert-only notification.
	   self.myScheduleAlertNotification()
   }
   else {
      // Schedule a notification with a badge and sound.
      self.badgeAppAndPlaySound() 
   }
}
```

## 声明可操作的通知类型

Declaring Your Actionable Notification Types

https://developer.apple.com/documentation/usernotifications/declaring_your_actionable_notification_types

允许用户在不启动应用的情况下对通知进行反馈操作。

若要支持可操作的通知, 必须:

* 在启动时从 iOS 应用程序中声明一个或多个通知类别。
* 为通知类别分配适当的操作。
* 处理您注册的所有操作。
* 在生成通知时, 将类别标识符分配给通知有效负载。

### 1. 注册操作

```
// 注册操作和通知类型
// UNNotificationAction 普通的按钮反馈事件
// UNTextInputNotificationAction 用户输入文本反馈事件

// UNNotificationActionOptions.init(rawValue: 0) 黑色文字，点击不进入 App
// authenticationRequired 需要解锁后才能显示，点击不会进入 App
// destructive 红色文字，点击不会进入 App
// foreground 黑色文字，点击后进入 App

// identifier: MEETING_INVITATION 为本地推送或远程推送时的关键信息


// Define the custom actions.
let acceptAction = UNNotificationAction(identifier: "ACCEPT_ACTION",
      title: "Accept", 
      options: UNNotificationActionOptions(rawValue: 0))
let declineAction = UNNotificationAction(identifier: "DECLINE_ACTION",
      title: "Decline", 
      options: UNNotificationActionOptions(rawValue: 0))
// Define the notification type
let meetingInviteCategory = 
      UNNotificationCategory(identifier: "MEETING_INVITATION",
      actions: [acceptAction, declineAction], 
      intentIdentifiers: [], 
      hiddenPreviewsBodyPlaceholder: "",
      options: .customDismissAction)
// Register the notification type.
let notificationCenter = UNUserNotificationCenter.current()
notificationCenter.setNotificationCategories([meetingInviteCategory])
```

### 2.1 分配给本地操作

```
// MEETING_INVITATION 是注册时的 identifier
// UserInfo 是传递给反馈处理的内容

let content = UNMutableNotificationContent()
content.title = "Weekly Staff Meeting"
content.body = "Every Tuesday at 2pm"
content.userInfo = [
    "MEETING_ID" : meetingID, 
    "USER_ID" : userID 
]
content.categoryIdentifier = "MEETING_INVITATION"
```

### 2.2 远程通知

```
{
   “aps” : {
      “category” : “MEETING_INVITATION”
      “alert” : {
         “title” : “Weekly Staff Meeting”
         “body” : “Every Tuesday at 2pm”
      },
   },
   “MEETING_ID” : “123456789”,
   “USER_ID” : “ABCD1234”
} 
```

### 3. 处理反馈操作

```
func userNotificationCenter(_ center: UNUserNotificationCenter,
       didReceive response: UNNotificationResponse,
       withCompletionHandler completionHandler: 
         @escaping () -> Void) {
       
   // Get the meeting ID from the original notification.
   let userInfo = response.notification.request.content.userInfo
   let meetingID = userInfo["MEETING_ID"] as! String
   let userID = userInfo["USER_ID"] as! String
        
   // Perform the task associated with the action.
   switch response.actionIdentifier {
   case "ACCEPT_ACTION":
      sharedMeetingManager.acceptMeeting(user: userID, 
                                    meetingID: meetingID)
      break
        
   case "DECLINE_ACTION":
      sharedMeetingManager.declineMeeting(user: userID, 
                                     meetingID: meetingID)
      break
        
   // Handle other actions…
 
   default:
      break
   }
    
   // Always call the completion handler when done.    
   completionHandler()
}
```

## 本地推送

### 1. 创建通知内容

```
let content = UNMutableNotificationContent()
content.title = "Weekly Staff Meeting"
content.body = "Every Tuesday at 2pm"
```

### 2. 指定提交条件

```
// 通过不同的提交条件，指定提醒功能
// UNCalendarNotificationTrigger 按日历提醒
// UNTimeIntervalNotificationTrigger 按时间提醒
// UNLocationNotificationTrigger 按地址位置提醒

// 每周二 2 点发送通知
var dateComponents = DateComponents()
dateComponents.calendar = Calendar.current

dateComponents.weekday = 3  // Tuesday
dateComponents.hour = 14    // 14:00 hours
   
// Create the trigger as a repeating event.    
let trigger = UNCalendarNotificationTrigger(
         dateMatching: dateComponents, repeats: true)
```

### 3. 创建和注册请求

```
// Create the request
let uuidString = UUID().uuidString
let request = UNNotificationRequest(identifier: uuidString, 
            content: content, trigger: trigger)

// Schedule the request with the system.
let notificationCenter = UNUserNotificationCenter.current()
notificationCenter.add(request) { (error) in
   if error != nil {
      // Handle any errors.
   }
}
```

### 4. 取消通知

```
center.removeAllPendingNotificationRequests()
center.removePendingNotificationRequests(withIdentifiers: ["通知请求"])
```


# Demo

## 推送带选项的通知

```

import UserNotifications

let center = UNUserNotificationCenter.current()
center.delegate = self
   
// 1. 事件
let done_action = UNNotificationAction(
  identifier: "Done_Action",
  title: "完成",
  options: UNNotificationActionOptions.init(rawValue: 0)
)
let continue_action = UNNotificationAction(
  identifier: "Continue_Action",
  title: "继续",
  options: UNNotificationActionOptions.init(rawValue: 0)
)
let text = UNTextInputNotificationAction(
  identifier: "Input",
  title: "输入",
  options: UNNotificationActionOptions.init(rawValue: 0)
)
   
// 2. 生成属性
let category = UNNotificationCategory(
  identifier: "Return_Notification",
  actions: [done_action, continue_action, text],
  intentIdentifiers: [],
  hiddenPreviewsBodyPlaceholder: "",
  options: .customDismissAction
)
// 3. 注册属性
center.setNotificationCategories([category])
   
// 4. 推送通知
let alert_content = UNMutableNotificationContent()
alert_content.title = "测试通知标题"
alert_content.body  = "测试通知的内容，可以长一点。"
alert_content.userInfo = ["Date": "OK"] // 传递数据
alert_content.categoryIdentifier = "Return_Notification"
   
// 多久之后进行推送，如果要重复，至少要 60 秒之后
let trigger = UNTimeIntervalNotificationTrigger(
  timeInterval: 10,
  repeats: false
)

let request = UNNotificationRequest(
  identifier: "通知请求",
  content: alert_content,
  trigger: trigger
)

center.add(request, withCompletionHandler: { (error) in
  // 成功添加推送
  print("add request success \(String(describing: error))")
})
        

// MARK: - UNUserNotificationCenterDelegate
    
// 接收到通知时应用反馈时的处理
func userNotificationCenter(_ center: UNUserNotificationCenter, didReceive response: UNNotificationResponse, withCompletionHandler completionHandler: @escaping () -> Void) {
   let info = response.notification.request.content.userInfo
   let date = info["Date"] as! String
   switch response.actionIdentifier {
   case "Continue_Action":
       print("Continue_Action return \(date)")
   case "Input":
       print("Input return \(date)")
       if let input = response as? UNTextInputNotificationResponse {
           print(input.userText)
       }
   case "Done_Action":
       print("Done_Action return \(date)")
   default: break
   }
   completionHandler()
}
    
// 接收到通知时应用在前台的处理
func userNotificationCenter(_ center: UNUserNotificationCenter, willPresent notification: UNNotification, withCompletionHandler completionHandler: @escaping (UNNotificationPresentationOptions) -> Void) {
   /** 处理通知 */
   print("userNotificationCenter \(notification)")
   /** 处理完后调用 */
   // UNNotificationPresentationOptions(rawValue: 0) 表示不作处理
   completionHandler(.alert)
}

    
```

## 推送普通通知

```
let center = UNUserNotificationCenter.current()
// 1. 获取权限
/**
.badge // 小红点
.sound // 声音
.alert // 警告
.carPlay // 车上播放
*/
center.requestAuthorization(
  options: [.badge, .sound, .alert],
  completionHandler: { (granted, error) in // 允许? 错误
      if granted {
          print("允许")
      } else {
          print("拒绝")
      }
})

// 2. 检查权限
center.getNotificationSettings(completionHandler: { (settings) in
  // 如果不允许，则不应该进行操作
  guard settings.authorizationStatus == .authorized else {return}

  if settings.badgeSetting == .enabled { print("badgeSetting") }
  if settings.soundSetting == .enabled { print("soundSetting") }
  if settings.alertSetting == .enabled { print("alertSetting") }
})

// 3. 推送通知
let alert_content = UNMutableNotificationContent()
alert_content.title = "测试通知标题"
alert_content.body  = "测试通知的内容，可以长一点。"
alert_content.sound = UNNotificationSound.default() // 声音

// 多久之后进行推送，如果要重复，至少要 60 秒之后
let trigger = UNTimeIntervalNotificationTrigger(
  timeInterval: 60,
  repeats: true
)

let request = UNNotificationRequest(
  identifier: "通知请求",
  content: alert_content,
  trigger: trigger
)


center.add(request, withCompletionHandler: { (error) in
  // 成功添加推送
  print("add request success \(String(describing: error))")
})

// 移除通知
center.removeAllPendingNotificationRequests()
center.removePendingNotificationRequests(withIdentifiers: ["通知请求"])

// MARK: - UNUserNotificationCenterDelegate
    
// 接收到通知时应用反馈时的处理
func userNotificationCenter(_ center: UNUserNotificationCenter, didReceive response: UNNotificationResponse, withCompletionHandler completionHandler: @escaping () -> Void) {
   let info = response.notification.request.content.userInfo
   let date = info["Date"] as! String
   switch response.actionIdentifier {
   case "Continue_Action":
       print("Continue_Action return \(date)")
   case "Input":
       print("Input return \(date)")
       if let input = response as? UNTextInputNotificationResponse {
           print(input.userText)
       }
   case "Done_Action":
       print("Done_Action return \(date)")
   default: break
   }
   completionHandler()
}
    
// 接收到通知时应用在前台的处理
func userNotificationCenter(_ center: UNUserNotificationCenter, willPresent notification: UNNotification, withCompletionHandler completionHandler: @escaping (UNNotificationPresentationOptions) -> Void) {
   /** 处理通知 */
   print("userNotificationCenter \(notification)")
   /** 处理完后调用 */
   // UNNotificationPresentationOptions(rawValue: 0) 表示不作处理
   completionHandler(.alert)
}

    
```

