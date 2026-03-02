# 当前 Agent 结构总结

## 总览

当前系统中有 **5 个独立的 Agent**，每个 Agent 都有：
- 独立的 workspace 目录
- 独立的配置文件
- 独立的会话管理
- 不同的飞书应用凭证

## Agent 列表

### 1. main (默认 Agent)
- **Agent ID**: main
- **Agent 目录**: `/root/.openclaw/agents/main`
- **Workspace**: `/root/.openclaw/workspace`
- **Agent Dir**: `/root/.openclaw/agents/main/agent`
- **模型**: zai/glm-4.7-flash
- **状态**: ✅ 活跃

### 2. agent1
- **Agent ID**: agent1
- **Agent 目录**: `/root/.openclaw/agents/agent1`
- **Workspace**: `/root/.openclaw/workspace-agent1`
- **Agent Dir**: `/root/.openclaw/agents/agent1/agent`
- **模型**: zai/glm-4.7-flash
- **飞书应用**: cli_a9282e3648381bcd
- **允许用户**: ou_bd188acc58f00b0b9d0677ad37aa0c85
- **状态**: ✅ 活跃

### 3. agent2
- **Agent ID**: agent2
- **Agent 目录**: `/root/.openclaw/agents/agent2`
- **Workspace**: `/root/.openclaw/workspace-agent2`
- **Agent Dir**: `/root/.openclaw/agents/agent2/agent`
- **模型**: zai/glm-4.7-flash
- **飞书应用**: cli_a929b17a71781bc0
- **允许用户**: ou_bd188acc58f00b0b9d0677ad37aa0c85
- **状态**: ✅ 活跃

### 4. agent3
- **Agent ID**: agent3
- **Agent 目录**: `/root/.openclaw/agents/agent3`
- **Workspace**: `/root/.openclaw/workspace-agent3`
- **Agent Dir**: `/root/.openclaw/agents/agent3/agent`
- **模型**: zai/glm-4.7-flash
- **飞书应用**: cli_a92ff88f1eb51cc4
- **允许用户**: ou_bd188acc58f00b0b9d0677ad37aa0c85
- **状态**: ✅ 活跃
- **子 Agent 限制**: 只能调用 agent1 和 agent2

### 5. assistant
- **Agent ID**: assistant
- **Agent 目录**: `/root/.openclaw/agents/assistant`
- **Workspace**: `/root/.openclaw/workspace-assistant`
- **Agent Dir**: `/root/.openclaw/agents/assistant/agent`
- **模型**: zai/glm-5
- **状态**: ✅ 活跃

## 目录结构

```
/root/.openclaw/agents/
├── main/                      # Agent 1
│   ├── agent/                # Agent 配置目录
│   │   ├── config.json
│   │   ├── auth-profiles.json
│   │   └── auth.json
│   └── sessions/             # 会话文件
│       ├── sessions.json
│       └── *.jsonl
├── agent1/                    # Agent 2
│   ├── agent/
│   └── sessions/
├── agent2/                    # Agent 3
│   ├── agent/
│   └── sessions/
├── agent3/                    # Agent 4
│   ├── agent/
│   └── sessions/
└── assistant/                 # Agent 5
    ├── agent/
    └── sessions/
```

## 飞书应用配置

| Agent | AppID | 应用名称 |
|-------|-------|----------|
| agent1 | cli_a9282e3648381bcd | Agent1 |
| agent2 | cli_a929b17a71781bc0 | Agent2 |
| agent3 | cli_a92ff88f1eb51cc4 | Agent3 |

## 工作原理

### 消息路由
1. 用户发送消息时，系统根据消息来源路由到相应的 agent
2. 每个 agent 有独立的飞书应用凭证
3. 每个 agent 有独立的 workspace 和会话

### Agent 3 的特殊配置
- **子 Agent 限制**: agent3 只能调用 agent1 和 agent2
- **工具限制**: 只允许 sessions_spawn, subagents, sessions_list, sessions_history, sessions_send
- **模型**: glm-4.7-flash

### 子 Agent 配置
- **允许的子 Agent**: agent1, agent2
- **模型**: zai/glm-4.7-flash
- **工具限制**: 只允许 sessions_spawn, sessions_send, sessions_list, sessions_history, read, write, exec
- **禁止工具**: gateway, cron

## 配置文件位置

- **主配置**: `/root/.openclaw/openclaw.json`
- **Agent 会话**: `/root/.openclaw/agents/{agentId}/sessions/sessions.json`

## 状态检查命令

```bash
# 查看服务状态
systemctl --user status openclaw-gateway.service

# 查看日志
journalctl --user -u openclaw-gateway.service -f

# 查看特定 agent 的会话
cat /root/.openclaw/agents/agent1/sessions/sessions.json
```

## 创建时间
- **main**: 2026-02-21
- **agent1**: 2026-03-02 14:11
- **agent2**: 2026-03-02 14:13
- **agent3**: 2026-03-02 16:49
- **assistant**: 2026-03-02 12:50

## 最后更新
- 2026年3月2日 23:20
