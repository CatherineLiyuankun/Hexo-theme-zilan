---
title: IOS日历同步到提醒事项-自动脚本
catalog: true
date: 2023-08-30 17:54:59
subtitle:
header-img:
tags:
---

根据知乎上的文章修改为自己的需求， 2023年最新的IOS16.6是正常执行的。

知乎上的文章：

## [【ios】日历同步---》提醒事项 单向同步+打卡功能 【作者：汀力】](https://zhuanlan.zhihu.com/p/169566930)

<details>
  <summary>代码1</summary>
  <p>

```javascript
// 1
var dur_month = 1;

const startDate = new Date();
startDate.setMonth(startDate.getMonth() - dur_month);
console.log(`日历的开始时间 ${startDate.toLocaleDateString()}`);

const endDate = new Date();
endDate.setMonth(endDate.getMonth() + dur_month);
console.log(`日历的结束时间 ${endDate.toLocaleDateString()}`);

const reminders = await Reminder.allDueBetween(startDate, endDate);
console.log(`获取 ${reminders.length} 条提醒事项`);

var calendar = await Calendar.forEvents();

// 获取日历名和对应的日历
var m_dict = {};
for (cal of calendar) {
  m_dict[cal.title] = cal;
  // console.log(`日历:${cal.title}`)
}

const events = await CalendarEvent.between(startDate, endDate, calendar);
console.log(`获取 ${events.length} 条日历`);

var reminders_id_set = new Set(reminders.map((e) => e.identifier));
// 删除日历里提醒事项删除的事项
events_created = events.filter(
  (e) => e.notes != null && e.notes.includes("[Reminder]")
);
for (let event of events_created) {
  // console.warn(event.notes)
  let reg = /(\[Reminder\])\s([A-Z0-9\-]*)/;
  let r = event.notes.match(reg);
  // if(r) console.log(r[2])
  if (!reminders_id_set.has(r[2])) {
    event.remove();
  }
}

for (const reminder of reminders) {
  // reminder的标识符
  const targetNote = `[Reminder] ${reminder.identifier}`;
  const [targetEvent] = events.filter(
    (e) => e.notes != null && e.notes.includes(targetNote)
  ); // 过滤重复的reminder
  if (!m_dict[reminder.calendar.title]) {
    console.warn("找不到日历" + reminder.calendar.title);
    continue;
  }
  if (targetEvent) {
    // console.log(`找到已经创建的事项 ${reminder.title}`)
    updateEvent(targetEvent, reminder);
  } else {
    console.warn(`创建事项 ${reminder.title} 到 ${reminder.calendar.title}`);
    const newEvent = new CalendarEvent();
    newEvent.notes = targetNote + "\n" + reminder.notes; // 要加入备注
    updateEvent(newEvent, reminder);
  }
}

Script.complete();

function updateEvent(event, reminder) {
  event.title = `${reminder.title}`;
  cal_name = reminder.calendar.title;
  cal = m_dict[cal_name];
  event.calendar = cal;
  // console.warn(event.calendar.title)
  // 已完成事项
  if (reminder.isCompleted) {
    event.title = `✅${reminder.title}`;
    //    event.isAllDay = false
    //     event.startDate = reminder.dueDate
    //   event.endDate=reminder.dueDate
    //    var ending = new Date(reminder.completionDate)
    //    ending.setHours(ending.getHours()+1)
    //    event.endDate = ending

    var period =
      (reminder.dueDate - reminder.completionDate) / 1000 / 3600 / 24;
    period = period.toFixed(1);
    if (period < 0) {
      period = -period;
      event.location = " 延期" + period + "天完成";
    } else if (period == 0) {
      event.location = " 准时完成";
    } else {
      event.location = " 提前" + period + "天完成";
    }
  }
  // 未完成事项
  else {
    const nowtime = new Date();
    var period = (reminder.dueDate - nowtime) / 1000 / 3600 / 24;
    period = period.toFixed(1);
    // console.log(reminder.title+(period))
    if (period < 0) {
      // 待办顺延

      event.location = " 延期" + -period + "天";
      // 如果不是在同一天,设置为全天事项
      if (reminder.dueDate.getDate() != nowtime.getDate()) {
        event.title = `❌${reminder.title}`;
        event.startDate = nowtime;
        event.endDate = nowtime;
        event.isAllDay = true;
      }
      // 在同一天的保持原来的时间
      else {
        event.title = `⭕️${reminder.title}`;
        event.isAllDay = false;
        event.startDate = reminder.dueDate;
        var ending = new Date(reminder.dueDate);
        ending.setHours(ending.getHours() + 1);
        event.endDate = ending;
      }
      console.log(`【${reminder.title}】待办顺延${-period}天`);
    } else {
      event.title = `⭕️${reminder.title}`;
      event.isAllDay = false;
      event.location = "还剩" + period + "天";
      event.startDate = reminder.dueDate;
      var ending = new Date(reminder.dueDate);
      ending.setHours(ending.getHours() + 1);
      event.endDate = ending;
    }
    if (!reminder.dueDateIncludesTime) event.isAllDay = true;
  }
  event.save();
}

```

  </p>
</details>

## [最完美(ios)提醒事项与日历  双向同步+带跳转  【作者：你说】（根据汀力）](https://zhuanlan.zhihu.com/p/558267163)

<details>
  <summary>代码2</summary>
  <p>

```javascript
// 2
var dur_month = 1;

const startDate = new Date();
startDate.setMonth(startDate.getMonth() - dur_month);
console.log(`日历的开始时间 ${startDate.toLocaleDateString()}`);

const endDate = new Date();
endDate.setMonth(endDate.getMonth() + dur_month);
console.log(`日历的结束时间 ${endDate.toLocaleDateString()}`);

event_cals = await Calendar.forEvents();
reminder_cals = await Calendar.forReminders();
titles = reminder_cals.map(e => e.title).filter(v => event_cals.map(e => e.title).includes(v));
console.log(`日历列表:${titles}`);

event_cals = event_cals.filter(v => titles.includes(v.title));
reminder_cals = reminder_cals.filter(v => titles.includes(v.title));

reminder_map = {};
reminder_cals.forEach(r => (reminder_map[r.title] = r));
// 时间范围过滤
const events = await CalendarEvent.between(startDate, endDate, event_cals);
const reminders = await Reminder.allDueBetween(startDate, endDate, reminder_cals);

//找出没有创建对应reminder的event，创建reminder
reminder_created = reminders.filter(e => e.priority == 1);
reminder_id_set = new Set(reminder_created.map(e => e.identifier));

reg = /(\\[id\\])x\\-apple\\-reminderkit\\:\\\/\\\/REMCDReminder\\\/([A-Z0-9\\-\\:\/=]*)$/;
// 提醒和日历 备注都要以[id]xxxxxx结尾
events.forEach(e => {
  if (e.notes != null) {
    s = e.notes.match(reg);
    if (s != null) {
      r_id = s[2];
    } else {
      r_id = "";
    }
  } else {
    r_id = '';
  }
  //console.log(e.title)
  if (e.title.startsWith("✅")) {
    event_ok = true;
    pure_title = e.title.substr(1);
  } else if (e.title.startsWith("☑️")) {
    event_ok = false;
    pure_title = e.title.substr(1);
  } else {
    event_ok = false;
    pure_title = e.title;
  }
  //console.log(''+event_ok)
  var r = undefined;
  if (!reminder_id_set.has(r_id)) {
    // 新创建状态来自日历标题
    remind_ok = event_ok;
    newReminder = new Reminder();
    newReminder.dueDate = e.startDate;
    newReminder.calendar = reminder_map[e.calendar.title];
    newReminder.dueDateIncludesTime = !e.isAllDay;
    newReminder.title = pure_title;
    newReminder.priority = 1;
    newReminder.isCompleted = remind_ok;
    newReminder.save();
    targetNote = `[id]x-apple-reminderkit:\/\/REMCDReminder\/${newReminder.identifier}`;
    console.log(`创建提醒:${pure_title}`);
    r = newReminder;
  } else {
    let [targetReminder] = reminder_created.filter(e => e.identifier == r_id);
    if (targetReminder.isCompleted) {
      remind_ok = true;
    } else {
      remind_ok = false;
    }
    // 标题参考日历的，状态参数提醒的
    targetReminder.title = pure_title;
    targetReminder.dueDate = e.startDate;
    targetReminder.dueDateIncludesTime = !e.isAllDay;
    targetReminder.save();
    console.log(`更新提醒:${pure_title}`);
    // 清理已经更新过的，用于后面删除日历上删除的
    targetNote = `[id]x-apple-reminderkit:\/\/REMCDReminder\/${targetReminder.identifier}`;
    reminder_id_set.delete(r_id);
    r = targetReminder;
  }
  if (remind_ok) {
    e.title = "✅" + pure_title;
  } else {
    e.title = "☑️" + pure_title;
  }
  //console.log(pure_title)
  if (e.notes == null) {
    e.notes = "\\r\\n\\r\\n" + targetNote;
  } else if (!e.notes.endsWith(targetNote)) {
    e.notes = e.notes + "\\r\\n\\r\\n" + targetNote;
  }
  // 如果不要打卡时间，注释掉
  updateEvent(e, r);
  e.save();
});

//reminder_id_set.forEach(v => {
//  console.log(`reminder:${v}`)
//})

reminder_id_set.forEach(id => {
  let [targetReminder] = reminder_created.filter(e => e.identifier == id);
  console.log(`删除提醒:${targetReminder.title}`);
  targetReminder.remove();
});

function updateEvent(event, reminder) {
  // 用户自定义的保持原样
  if (event.location != null && !event.location.startsWith("⏱")) {
  }
  //已完成事项
  else if (reminder.isCompleted) {
    var period = (reminder.dueDate - reminder.completionDate) / 1000 / 3600 / 24;
    period = period.toFixed(1);
    if (period < 0) {
      period = -period;
      event.location = "⏱延期" + period + "天完成";
    } else if (period == 0) {
      event.location = "⏱准时完成";
    } else {
      event.location = "⏱提前" + period + "天完成";
    }
  //未完成事项
  } else {
    const nowtime = new Date();
    var period = (reminder.dueDate - nowtime) / 1000 / 3600 / 24;
    period = period.toFixed(1);
    //console.log(reminder.title+(period))
    if (period < 0) {
      event.location = "⏱延期" + (-period) + "天";
    } else {
      event.location = "⏱还剩" + period + "天";
    }
  }
}

Script.complete();


// 首先，定义了一个变量 dur_month，它被设置为1。这个变量可能用于计算日期范围。
// 接下来，创建了两个日期对象 startDate 和 endDate，它们表示日历的开始时间和结束时间。这些日期根据 dur_month 进行调整。
// 代码使用了 await 关键字来等待获取日历事件和提醒事件的数据。它使用 Calendar.forEvents() 和 Calendar.forReminders() 方法来获取事件和提醒的列表。
// 通过比较提醒和事件的标题，创建了一个名为 titles 的数组，其中包含在日历和提醒中都存在的标题。这个数组用于筛选出共有的事件和提醒。
// 接下来，对事件和提醒的列表进行过滤，只保留 titles 数组中存在的事件和提醒。
// 创建了一个空对象 reminder_map，用于将提醒的标题映射到提醒对象。
// 使用正则表达式 reg 匹配提醒和事件的备注，以提取提醒的唯一标识符。
// 遍历事件列表，处理每个事件的逻辑。根据事件标题的前缀（"✅" 或 "☑️"），确定事件是否已完成，并提取纯标题。然后，检查是否存在相应的提醒。如果不存在，创建新的提醒，并将其关联到事件上。如果存在，更新现有的提醒。
// 最后，根据提醒的状态更新事件标题，并将提醒的标识符添加到事件的备注中。还有一些与事件位置相关的逻辑。
// 最后，使用 Script.complete() 结束脚本的执行。



```

  </p>
</details>

## [自动同步iOS提醒事项到日历？简单，看这里！  【作者：crazy】 （根据汀力+你说）](https://zhuanlan.zhihu.com/p/539872086)

## 我的改动和代码

根据[汀力](https://zhuanlan.zhihu.com/p/169566930)最新的那篇，发现了几个和我自己需求不符合的点：

- 从reminder 新建到calendar的event默认1小时
  - 在calendar中修改event的开始时间和结束时间，执行脚本后会被重新改成reminder的开始时间，结束时间固定为1小时。
- reminder 里面删除后，calendar里面还有（不会被删除）
  - 这个是个bug?看代码里面是有这个逻辑的

我的需求和修改

- 如果calendar 已有reminder相同title的event，不update，所以可以在calendar中修改event的开始时间和结束时间
  - 如果calendar里面已经有event了，修改reminder里面的时间为calendar event的开始时间间
- 【已完成】 不会变成全天任务， 仍然是有开始时间和结束时间

<details>
  <summary>代码3</summary>
  <p>

```javascript
// 3

// LYK 创建 EventKit 实例
// const EventKit = require("EventKit");
// const eventKit = EventKit.init();

var dur_month = 1;

const startDate = new Date();
startDate.setMonth(startDate.getMonth() - dur_month);
console.log(`日历的开始时间 ${startDate.toLocaleDateString()}`);

const endDate = new Date();
endDate.setMonth(endDate.getMonth() + dur_month);
console.log(`日历的结束时间 ${endDate.toLocaleDateString()}`);

const reminders = await Reminder.allDueBetween(startDate, endDate);
console.log(`获取 ${reminders.length} 条提醒事项`);

var calendar = await Calendar.forEvents();

// 获取日历名和对应的日历
var m_dict = {};
for (cal of calendar) {
  m_dict[cal.title] = cal;
  // console.log(`日历:${cal.title}`)
}

const events = await CalendarEvent.between(startDate, endDate, calendar);
console.log(`获取 ${events.length} 条日历`);

var reminders_id_set = new Set(reminders.map((e) => e.identifier));
// 删除日历里提醒事项删除的事项
events_created = events.filter(
  (e) => e.notes != null && e.notes.includes("[Reminder]")
);
for (let event of events_created) {
  // console.warn(event.notes)
  let reg = /(\[Reminder\])\s([A-Z0-9\-]*)/;
  let r = event.notes.match(reg);
  // if(r) console.log(r[2])
  if (!reminders_id_set.has(r[2])) {
    event.remove();
  }
}

for (const reminder of reminders) {
  // reminder的标识符
  const targetNote = `[Reminder] ${reminder.identifier}`;
  const [targetEvent] = events.filter(
    (e) => e.notes != null && e.notes.includes(targetNote)
  ); // 过滤重复的reminder
  if (!m_dict[reminder.calendar.title]) {
    console.warn("找不到日历" + reminder.calendar.title);
    continue;
  }
  if (targetEvent) {
    // console.log(`找到已经创建的事项 ${reminder.title}`)
    
    // LYK 替换updateEvent为updateReminder
    // updateEvent(targetEvent, reminder);
    updateReminder(targetEvent, reminder);
  } else {
    console.warn(`创建事项 ${reminder.title} 到 ${reminder.calendar.title}`);
    const newEvent = new CalendarEvent();
    newEvent.notes = targetNote + "\n" + reminder.notes; // 要加入备注
    updateEvent(newEvent, reminder);
  }
}

// LYK 方法2 EventKit方法
// 添加事件修改监听器
//   for (const event of events) {
//     event.onStartDateChange(() => {
//       // 在这里实现日历事件开始时间更改时的同步操作
//       // 可以获取修改后的开始时间，然后更新对应的 Reminder 提醒

//       // 找到对应的 Reminder
//       const targetNote = `[Reminder] ${event.notes
//         .split("\n")[0]
//         .substring(10)}`;
//       const reminderToUpdate = reminders.find(
//         (reminder) => reminder.identifier === targetNote
//       );

//       if (reminderToUpdate) {
//         // 更新 Reminder 的开始时间
//         reminderToUpdate.dueDate = event.startDate;
//         // 保存 Reminder 更新
//         eventKit.saveReminder(reminderToUpdate, (error) => {
//           if (!error) {
//             console.log(`已同步更新 Reminder 的开始时间为 ${event.startDate}`);
//           } else {
//             console.error(`更新 Reminder 失败：${error}`);
//           }
//         });
//       }
//     });

//     event.onEndDateChange(() => {
//       // 在这里实现日历事件结束时间更改时的同步操作
//       // 可以获取修改后的结束时间，然后更新对应的 Reminder 提醒

//       // 找到对应的 Reminder
//       const targetNote = `[Reminder] ${event.notes
//         .split("\n")[0]
//         .substring(10)}`;
//       const reminderToUpdate = reminders.find(
//         (reminder) => reminder.identifier === targetNote
//       );

//       if (reminderToUpdate) {
//         // 更新 Reminder 的结束时间
//         reminderToUpdate.dueDate = event.endDate;
//         // 保存 Reminder 更新
//         eventKit.saveReminder(reminderToUpdate, (error) => {
//           if (!error) {
//             console.log(`已同步更新 Reminder 的结束时间为 ${event.endDate}`);
//           } else {
//             console.error(`更新 Reminder 失败：${error}`);
//           }
//         });
//       }
//     });
//   }

Script.complete();

function updateEvent(event, reminder) {
  event.title = `${reminder.title}`;
  cal_name = reminder.calendar.title;
  cal = m_dict[cal_name];
  event.calendar = cal;
  // console.warn(event.calendar.title)
  // 已完成事项
  if (reminder.isCompleted) {
    event.title = `✅${reminder.title}`;
    //    event.isAllDay = false
    //     event.startDate = reminder.dueDate
    //   event.endDate=reminder.dueDate
    //    var ending = new Date(reminder.completionDate)
    //    ending.setHours(ending.getHours()+1)
    //    event.endDate = ending

    var period =
      (reminder.dueDate - reminder.completionDate) / 1000 / 3600 / 24;
    period = period.toFixed(1);
    if (period < 0) {
      period = -period;
      event.location = " 延期" + period + "天完成";
    } else if (period == 0) {
      event.location = " 准时完成";
    } else {
      event.location = " 提前" + period + "天完成";
    }
  }
  // 未完成事项
  else {
    const nowtime = new Date();
    var period = (reminder.dueDate - nowtime) / 1000 / 3600 / 24;
    period = period.toFixed(1);
    // console.log(reminder.title+(period))
    if (period < 0) {
      // 待办顺延

      event.location = " 延期" + -period + "天";
      // 如果不是在同一天,设置为全天事项
      if (reminder.dueDate.getDate() != nowtime.getDate()) {
        event.title = `❌${reminder.title}`;
        event.startDate = nowtime;
        event.endDate = nowtime;
        event.isAllDay = true;
      }
      // 在同一天的保持原来的时间
      else {
        event.title = `⭕️${reminder.title}`;
        event.isAllDay = false;
        event.startDate = reminder.dueDate;
        var ending = new Date(reminder.dueDate);
        ending.setHours(ending.getHours() + 1);
        event.endDate = ending;
      }
      console.log(`【${reminder.title}】待办顺延${-period}天`);
    } else {
      event.title = `⭕️${reminder.title}`;
      event.isAllDay = false;
      event.location = "还剩" + period + "天";
      event.startDate = reminder.dueDate;
      var ending = new Date(reminder.dueDate);
      ending.setHours(ending.getHours() + 1);
      event.endDate = ending;
    }
    if (!reminder.dueDateIncludesTime) event.isAllDay = true;
  }
  event.save();
}

// LYK 新加的方法
function updateReminder(event, reminder) {
  // 方法1
  if (reminder) {
    // 更新 Reminder 的开始时间
    reminder.dueDate = event.startDate;
    // 保存 Reminder 更新
    reminder.save();
  }
}

```

  </p>
</details>

## 参考文章

1. 【ios】日历同步---》提醒事项 单向同步+打卡功能 【作者：汀力】

- <https://zhuanlan.zhihu.com/p/390100397> 2021.7
- <https://zhuanlan.zhihu.com/p/169566930> 2022.9.17

2. 最完美(ios)提醒事项与日历  双向同步+带跳转  【作者：你说】（根据汀力）

- <https://zhuanlan.zhihu.com/p/512921323> 2022.8
- <https://zhuanlan.zhihu.com/p/558267163> 2022.9.19
双向同步v3.scriptable

3. 自动同步iOS提醒事项到日历？简单，看这里！  【作者：crazy】 （根据汀力+你说）

- <https://zhuanlan.zhihu.com/p/539872086>  2022.7

4. [将 iOS 上的提醒事项同步到微软日历](https://zhuanlan.zhihu.com/p/335275758)
