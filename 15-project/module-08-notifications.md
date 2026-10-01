# Module 8: Notifications

## Requirement
In-app notifications (toast + notification list with unread count).

## Options
- A) Polling (`refetchInterval` React Query): simple.
- B) Laravel Broadcasting + Echo/Pusher: real-time, setup heavy.
- C) Server-Sent Events: one-way real-time.

Start with polling (simple requirement), real-time tab justify ho tab.

## Implementation
```jsx
const { data } = useQuery({ queryKey: ["notifications"], queryFn: notificationService.list, refetchInterval: 30000 });
const unread = data?.filter(n => !n.read_at).length ?? 0;
```
Laravel: `$user->notifications`, `markAsRead()`.

## Task
Bell icon + unread badge + mark as read mutation + toast on create success.

## Interview Qs
- Polling vs WebSocket trade-offs?
