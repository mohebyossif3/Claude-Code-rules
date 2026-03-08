  You are setting up a complete user-level Claude Code environment so that EVERY project  
  and directory automatically gets claude-flow v3, multi-agent swarms, self-learning hooks,
  60+ agents, 100+ skills, MCP servers, and plugins.                                                                                                                                                                   
                                                                                                                                                                                                                       
  IMPORTANT: Everything must be at USER LEVEL (~/.claude/) not project level.
  Claude Code's hierarchy: user settings (~/.claude/settings.json) apply globally,
  project settings (.claude/settings.json) override per-project.

  ---

  ## PHASE 1: Global Prerequisites

  ```bash
  # Ensure claude-flow CLI is available globally
  npm install -g @claude-flow/cli@latest

  # Ensure ruflo is available (if using ruflo MCP)
  # npm install -g ruflo  # or however ruflo was installed

  # Install playwright MCP globally
  npm install -g playwright-mcp

  PHASE 2: User-Level MCP Servers (~/.claude/settings.json)

  MCP servers defined in ~/.claude/settings.json under mcpServers are available
  in ALL projects. This is the correct location for global MCPs.

  Create/update ~/.claude/settings.json:

  {
    "env": {
      "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1",
      "CLAUDE_FLOW_V3_ENABLED": "true",
      "CLAUDE_FLOW_HOOKS_ENABLED": "true"
    },
    "enabledPlugins": {
      "claude-session-driver@superpowers-marketplace": true,
      "superpowers-developing-for-claude-code@superpowers-marketplace": true,
      "frontend-design@claude-plugins-official": true,
      "double-shot-latte@superpowers-marketplace": true,
      "superpowers-chrome@superpowers-marketplace": true,
      "superpowers@claude-plugins-official": true
    },
    "skipDangerousModePermissionPrompt": true,
    "mcpServers": {
      "ruflo": {
        "command": "ruflo",
        "args": ["mcp"]
      },
      "claude-flow": {
        "command": "npx",
        "args": ["-y", "@claude-flow/cli@latest", "mcp", "start"],
        "env": {
          "npm_config_update_notifier": "false",
          "CLAUDE_FLOW_MODE": "v3",
          "CLAUDE_FLOW_HOOKS_ENABLED": "true",
          "CLAUDE_FLOW_TOPOLOGY": "hierarchical-mesh",
          "CLAUDE_FLOW_MAX_AGENTS": "15",
          "CLAUDE_FLOW_MEMORY_BACKEND": "hybrid"
        }
      },
      "playwright": {
        "command": "playwright-mcp",
        "args": ["--headless"]
      }
    },
    "permissions": {
      "allow": [
        "Bash(npx @claude-flow*)",
        "Bash(npx claude-flow*)",
        "Bash(node .claude/*)",
        "Bash(ruflo *)",
        "mcp__claude-flow__:*",
        "mcp__ruflo__:*"
      ],
      "deny": [
        "Read(./.env)",
        "Read(./.env.*)"
      ]
    },
    "hooks": {
      "SessionStart": [
        {
          "hooks": [
            {
              "type": "command",
              "command": "npx @claude-flow/cli@latest hooks session-start 2>/dev/null; node .claude/helpers/hook-handler.cjs session-restore 2>/dev/null || true",
              "timeout": 15000
            }
          ]
        }
      ],
      "SessionEnd": [
        {
          "hooks": [
            {
              "type": "command",
              "command": "node .claude/helpers/hook-handler.cjs session-end 2>/dev/null || true",
              "timeout": 10000
            }
          ]
        }
      ],
      "UserPromptSubmit": [
        {
          "hooks": [
            {
              "type": "command",
              "command": "node .claude/helpers/hook-handler.cjs route 2>/dev/null || true",
              "timeout": 10000
            }
          ]
        }
      ],
      "PreToolUse": [
        {
          "matcher": "Bash",
          "hooks": [
            {
              "type": "command",
              "command": "node .claude/helpers/hook-handler.cjs pre-bash 2>/dev/null || true",
              "timeout": 5000
            }
          ]
        },
        {
          "matcher": "Write|Edit|MultiEdit",
          "hooks": [
            {
              "type": "command",
              "command": "node .claude/helpers/hook-handler.cjs pre-edit 2>/dev/null || true",
              "timeout": 5000
            }
          ]
        }
      ],
      "PostToolUse": [
        {
          "matcher": "Write|Edit|MultiEdit",
          "hooks": [
            {
              "type": "command",
              "command": "node .claude/helpers/hook-handler.cjs post-edit 2>/dev/null || true",
              "timeout": 10000
            }
          ]
        },
        {
          "matcher": "Bash",
          "hooks": [
            {
              "type": "command",
              "command": "node .claude/helpers/hook-handler.cjs post-bash 2>/dev/null || true",
              "timeout": 5000
            }
          ]
        }
      ],
      "Stop": [
        {
          "hooks": [
            {
              "type": "command",
              "command": "node .claude/helpers/auto-memory-hook.mjs sync 2>/dev/null || true",
              "timeout": 10000
            }
          ]
        }
      ],
      "SubagentStart": [
        {
          "hooks": [
            {
              "type": "command",
              "command": "node .claude/helpers/hook-handler.cjs status 2>/dev/null || true",
              "timeout": 3000
            }
          ]
        }
      ],
      "SubagentStop": [
        {
          "hooks": [
            {
              "type": "command",
              "command": "node .claude/helpers/hook-handler.cjs post-task 2>/dev/null || true",
              "timeout": 5000
            }
          ]
        }
      ],
      "Notification": [
        {
          "hooks": [
            {
              "type": "command",
              "command": "node .claude/helpers/hook-handler.cjs notify 2>/dev/null || true",
              "timeout": 3000
            }
          ]
        }
      ]
    },
    "statusLine": {
      "type": "command",
      "command": "node .claude/helpers/statusline.cjs 2>/dev/null || echo 'claude-flow v3'"
    },
    "attribution": {
      "commit": "Co-Authored-By: claude-flow <ruv@ruv.net>",
      "pr": "🤖 Generated with [claude-flow](https://github.com/ruvnet/claude-flow)"
    },
    "claudeFlow": {
      "version": "3.0.0",
      "enabled": true,
      "platform": {"os": "linux", "arch": "x64", "shell": "bash"},
      "modelPreferences": {"default": "claude-opus-4-6", "routing": "claude-haiku-4-5-20251001"},
      "agentTeams": {
        "enabled": true,
        "teammateMode": "auto",
        "taskListEnabled": true,
        "mailboxEnabled": true,
        "coordination": {
          "autoAssignOnIdle": true,
          "trainPatternsOnComplete": true,
          "notifyLeadOnComplete": true,
          "sharedMemoryNamespace": "agent-teams"
        }
      },
      "swarm": {"topology": "hierarchical-mesh", "maxAgents": 15},
      "memory": {
        "backend": "hybrid",
        "enableHNSW": true,
        "learningBridge": {"enabled": true},
        "memoryGraph": {"enabled": true},
        "agentScopes": {"enabled": true}
      },
      "neural": {"enabled": true},
      "daemon": {
        "autoStart": true,
        "workers": ["map","audit","optimize","consolidate","testgaps","ultralearn","deepdive","document","refactor","benchmark"]
      },
      "learning": {
        "enabled": true,
        "autoTrain": true,
        "patterns": ["coordination","optimization","prediction"],
        "retention": {"shortTerm": "24h", "longTerm": "30d"}
      },
      "security": {"autoScan": true, "scanOnEdit": true, "cveCheck": true, "threatModel": true}
    }
  }

  IMPORTANT: The || true on every hook command is critical — it prevents hooks from
  failing in projects that haven't been initialized with claude-flow yet. Hooks gracefully
  degrade: they work in initialized projects and silently skip in others.

  PHASE 3: Install Plugins (User Level)

  These are installed globally and persist across all projects:

  claude plugin install claude-session-driver@superpowers-marketplace
  claude plugin install superpowers-developing-for-claude-code@superpowers-marketplace
  claude plugin install frontend-design@claude-plugins-official
  claude plugin install double-shot-latte@superpowers-marketplace
  claude plugin install superpowers-chrome@superpowers-marketplace
  claude plugin install superpowers@claude-plugins-official

  PHASE 4: Install Skills (User Level)

  Skills in ~/.claude/skills/ apply globally:

  claude skill install remotion-dev/skills
  claude skill install nichochar/vercel-react-best-practices

  PHASE 5: Global CLAUDE.md (~/.claude/CLAUDE.md)

  Create ~/.claude/CLAUDE.md with the full behavioral contract:

  Core Build Workflow

  Whenever I request software, scripts, tools, services, infrastructure, or applications:

  Use Ruffalo MCP as part of the development workflow whenever applicable.

  Do not stop at partial implementations.
  Continue working until a fully functional, production-ready product exists.

  Claude should follow a complete development lifecycle:
  Planning → Implementation → Quality assurance → End-to-end testing → Bug fixing → Final verification → Production-ready deployment

  Claude should iterate through these stages in development loops until the system is stable and reliable.
  Do not deliver unfinished prototypes or partially working systems.

  Quality Assurance and Testing

  Before a task is considered complete, Claude must ensure:
  - Functional testing
  - End-to-end testing
  - Error handling validation
  - Edge case coverage
  - Logging validation
  - Basic performance checks

  The resulting product must be ready for real-world use.

  Deployment and Accessibility

  When a web service, API, or application is created:
  - Deploy it so it is publicly accessible through a URL
  - Use Caddy as the reverse proxy
  - Use sslip.io domains (format: service-name.<IP>.sslip.io)
  - Automatic HTTPS using Caddy
  - Production mode, not development mode

  Logging Standards

  All generated software must include structured logging:
  - JSON formatted, file-based only (never databases)
  - Log levels: debug, info, warning, error
  - Storage: /logs directory with application.log, error.log, debug.log
  - Rotating log files with size limits and retention policies

  Frontend and UI Design

  - Framework: React
  - Light theme only (no dark themes unless explicitly requested)
  - Vercel-level design quality: clean, modern, elegant spacing, clear typography
  - Strong visual hierarchy, intuitive navigation

  Software Architecture

  - Design patterns: Adapter, Facade, Factory (when beneficial)
  - Modular, maintainable, well-structured, production-ready code
  - Clear naming, separation of concerns, scalable architecture
  - Logging as a first-class system component

  Server Access Permission

  Claude is permitted to: install software, configure services, deploy applications,
  set up infrastructure, execute administrative commands.
  Never store passwords or secrets in code or memory files.

  Completion Requirement

  A task is only complete when: product functions correctly, deployment works,
  URL works (if applicable), tests pass, logging is implemented, system behaves reliably.

  Claude-Flow Integration

  For any new project, initialize claude-flow:
    npx @claude-flow/cli@latest init --wizard
    npx @claude-flow/cli@latest daemon start
    npx @claude-flow/cli@latest doctor --fix

  This generates .claude/helpers, agents, commands, skills, and .swarm/ for the project.

  Swarm Rules:
  - Hierarchical topology, 6-8 agents max for tight coordination
  - Raft consensus, specialized strategy
  - Batch ALL agent spawns in ONE message
  - Always run_in_background for agent tasks
  - Never poll status — trust agents to return

  File Organization (per project):
  - /src for source code
  - /tests for test files
  - /docs for documentation
  - /config for configuration
  - /scripts for utility scripts
  - Never save to root folder

  PHASE 6: Per-Project Bootstrap Command

  When entering any new project, Claude should auto-initialize if .claude/ doesn't exist:

  # One-liner to bootstrap any project with claude-flow
  npx @claude-flow/cli@latest init --wizard && npx @claude-flow/cli@latest daemon start && npx @claude-flow/cli@latest doctor --fix

  This generates the project-level .claude/helpers/, .claude/agents/, .claude/commands/,
  .claude/skills/, and .swarm/ that the hooks reference.

  ---
  SELF-VALIDATION LOOP

  After completing all phases, enter this validation loop.
  DO NOT consider the task complete until ALL checks pass.

  Level 1: User-Level Checks (must work from ANY directory)

  # 1. Settings file exists and has MCP servers
  test -f ~/.claude/settings.json && echo "✓ settings.json" || echo "✗ MISSING"
  cat ~/.claude/settings.json | python3 -c "import sys,json; d=json.load(sys.stdin); print('✓ claude-flow MCP' if 'claude-flow' in d.get('mcpServers',{}) else '✗ claude-flow MCP MISSING')"
  cat ~/.claude/settings.json | python3 -c "import sys,json; d=json.load(sys.stdin); print('✓ ruflo MCP' if 'ruflo' in d.get('mcpServers',{}) else '✗ ruflo MCP MISSING')"

  # 2. Plugins installed
  cat ~/.claude/plugins/installed_plugins.json | python3 -c "
  import sys,json; d=json.load(sys.stdin)
  expected=['claude-session-driver@superpowers-marketplace','superpowers-developing-for-claude-code@superpowers-marketplace','frontend-design@claude-plugins-official','double-shot-latte@superpowers-marketplace','sup
  erpowers-chrome@superpowers-marketplace','superpowers@claude-plugins-official']
  for p in expected:
      print(f'  ✓ {p.split(\"@\")[0]}' if p in d.get('plugins',{}) else f'  ✗ {p} MISSING')
  "

  # 3. Global CLAUDE.md exists
  test -f ~/.claude/CLAUDE.md && echo "✓ CLAUDE.md" || echo "✗ CLAUDE.md MISSING"
  grep -q "production-ready" ~/.claude/CLAUDE.md && echo "  ✓ has lifecycle rules" || echo "  ✗ lifecycle rules MISSING"

  # 4. User-level skills
  ls ~/.claude/skills/ | while read s; do echo "  ✓ skill: $s"; done

  # 5. Hooks are defined in settings
  cat ~/.claude/settings.json | python3 -c "
  import sys,json; d=json.load(sys.stdin)
  hooks = d.get('hooks',{})
  for h in ['SessionStart','SessionEnd','UserPromptSubmit','PreToolUse','PostToolUse','Stop','SubagentStart','SubagentStop','Notification']:
      print(f'  ✓ hook: {h}' if h in hooks else f'  ✗ hook: {h} MISSING')
  "

  # 6. Env vars set
  cat ~/.claude/settings.json | python3 -c "
  import sys,json; d=json.load(sys.stdin)
  env = d.get('env',{})
  print('✓ AGENT_TEAMS enabled' if env.get('CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS')=='1' else '✗ AGENT_TEAMS MISSING')
  print('✓ V3 enabled' if env.get('CLAUDE_FLOW_V3_ENABLED')=='true' else '✗ V3 MISSING')
  print('✓ HOOKS enabled' if env.get('CLAUDE_FLOW_HOOKS_ENABLED')=='true' else '✗ HOOKS MISSING')
  "

  # 7. Permissions set
  cat ~/.claude/settings.json | python3 -c "
  import sys,json; d=json.load(sys.stdin)
  perms = d.get('permissions',{})
  print('✓ allow rules' if len(perms.get('allow',[])) >= 4 else '✗ allow rules MISSING')
  print('✓ deny .env' if any('.env' in r for r in perms.get('deny',[])) else '✗ deny .env MISSING')
  "

  Level 2: Project-Level Checks (from an initialized project)

  cd /opt/ruflo-workspace  # or any initialized project

  # Project-level claude-flow artifacts
  test -d .claude/helpers && echo "✓ helpers/" || echo "✗ helpers/ MISSING — run: npx @claude-flow/cli@latest init --wizard"
  test -d .claude/agents && echo "✓ agents/" || echo "✗ agents/ MISSING"
  test -d .claude/commands && echo "✓ commands/" || echo "✗ commands/ MISSING"
  test -d .claude/skills && echo "✓ skills/" || echo "✗ skills/ MISSING"
  test -d .swarm && echo "✓ .swarm/" || echo "✗ .swarm/ MISSING"
  test -f .claude/helpers/hook-handler.cjs && echo "✓ hook-handler.cjs" || echo "✗ hook-handler MISSING"

  # Component counts
  echo "Agents: $(find .claude/agents -name '*.md' 2>/dev/null | wc -l) (expect 80+)"
  echo "Skills: $(ls .claude/skills/ 2>/dev/null | wc -l) (expect 31+)"
  echo "Commands: $(find .claude/commands -name '*.md' 2>/dev/null | wc -l) (expect 70+)"
  echo "Helpers: $(ls .claude/helpers/ 2>/dev/null | wc -l) (expect 40+)"

  # MCP and daemon
  npx @claude-flow/cli@latest system status
  npx @claude-flow/cli@latest doctor --fix

  Level 3: Functional Tests

  # Memory round-trip
  npx @claude-flow/cli@latest memory store --key "setup-test" --value "pass" --namespace test
  npx @claude-flow/cli@latest memory retrieve --key "setup-test" --namespace test
  npx @claude-flow/cli@latest memory delete --key "setup-test" --namespace test

  # Agent lifecycle
  npx @claude-flow/cli@latest agent spawn -t coder --name validation-agent
  npx @claude-flow/cli@latest agent list
  npx @claude-flow/cli@latest agent terminate --name validation-agent

  # Swarm lifecycle
  npx @claude-flow/cli@latest swarm init --topology hierarchical --max-agents 8 --strategy specialized
  npx @claude-flow/cli@latest swarm status
  npx @claude-flow/cli@latest swarm shutdown

  Validation Loop Logic:

  1. Run Level 1 checks — if ANY fail, fix and re-run Level 1
  2. Run Level 2 checks — if ANY fail, run npx @claude-flow/cli@latest init --wizard && doctor --fix, re-run Level 2
  3. Run Level 3 checks — if ANY fail, diagnose, fix, re-run Level 3
  4. Only when ALL 3 levels pass with zero failures: report "Setup complete. All validations passed."
  5. DO NOT mark complete until the loop exits cleanly.
