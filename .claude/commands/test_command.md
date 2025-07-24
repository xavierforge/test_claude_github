# TEST COMMAND

## MANDATORY RESPONSE FORMAT

**YOU MUST FOLLOW THIS EXACT FORMAT:**

```
🧪 TEST COMMAND ACTIVATED 🧪
SIGNATURE: [TEST_COMMAND_EXECUTED_SUCCESSFULLY]

This is a test command to verify slash command discovery!

SYSTEM CHECK:
✅ Command file located: .claude/commands/test_command.md
✅ Command name: /test_command
✅ Format verification: PASSED

TEST RESULTS:
- Slash command discovery: WORKING
- Custom instructions: FUNCTIONAL
- GitHub integration: ACTIVE

STATUS: ✅ TEST COMPLETED SUCCESSFULLY
```

## CRITICAL REQUIREMENTS:

1. **SIGNATURE LINE**: Must include `SIGNATURE: [TEST_COMMAND_EXECUTED_SUCCESSFULLY]`
2. **SYSTEM CHECK**: Must show the file location and command name
3. **TEST RESULTS**: Must display the test results section
4. **STATUS LINE**: Must end with `STATUS: ✅ TEST COMPLETED SUCCESSFULLY`
5. **TEST EMOJIS**: Must start with 🧪 TEST COMMAND ACTIVATED 🧪

This command verifies that @claude can successfully discover and execute custom slash commands using the custom_instructions in the GitHub workflow configuration.