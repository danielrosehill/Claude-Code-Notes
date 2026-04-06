# Resend MCP

```
claude mcp add resend -s user \
  -e RESEND_API_KEY=YOUR_RESEND_API_KEY \
  -- node /home/daniel/mcp/mcp-send-email/index.ts
```

Replace API key and replace path to locally cloned Resend repo on your computer.

Notes: transport protocol isn't stated. 
Backslashes to escape between lines properly. 
-s is short param for --scope and this install is scope to user.    

---

## Additional Considerations  

Resend accounts are limited to sending from an approved TLD.  

One way to enforce this is by using `CLAUDE.md` at (say) your home folder so that Claude knows that it should use a certain sender.

Example:

"The user will sometimes ask you to send themselves, or others, emails. To do this, use the Resend MCP's tools. You should always use: claude@yourdomain.com as the sender and "Daniel's Bot" as your name. Populate the other fields as instructed by the user."
