# State giữa nhiều tab browser cần sync

- localStorage event
- BroadcastChannel
- Backend sync

## Chi tiết câu trả lời

Sync state across tabs.

### localStorage event

- Listen storage event.
- Update state khi other tab changes.

### BroadcastChannel

- Modern API cho inter-tab communication.
- Send/receive messages.

### Backend sync

- Persist state to server.
- Poll hoặc websocket sync.

Choose based on complexity và real-time needs.
