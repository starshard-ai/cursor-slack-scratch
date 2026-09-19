# Checklist: authorize Singapore hub pubkey + verify Signal

**Status:** Operator checklist (Cloud Fable, 2026-09-19). Run only after owner `go` on the matching OPEN-QS.
**Who runs it:** a principal already on the execution plane (owner, Mac frontstage, or Adam on Air/tokyo/Singapore). **Not** the shared Eden / Grok VM. **Not** this Cloud Agent.
**Surface note:** public. Role names only. **No secrets, no private keys, no mesh IPs, no machine ids, no message bodies.**

Parent: `SINGAPORE-HUB-BRIEF.md`. Questions: `SINGAPORE-HUB-OPEN-QS.md`.

---

## 0. Rules of the road

1. Print and move the **public** key only. If a command would display a private key, stop.
2. Do not paste key material, `authorized_keys` files, or `ssh-keygen` fingerprints into git, Hub memo bodies, Eden chat, or this repo.
3. Do not copy Air’s entire `~/.ssh` onto Singapore.
4. Do not install any private key onto the shared Eden / Grok VM.
5. Mesh visibility ≠ SSH authorization. A node can be listed and still say `Permission denied (publickey)`.
6. Singapore-loop (SSH to self) is **optional**. Do not block the rest of the list on it.
7. Pro / Hangzhou is **deferred** unless owner `go` includes it. Timeout today is expected.

Record results as **role + outcome** (`seoul: authorized`, `bangkok-mini: denied`, `Pro: skipped`). Not as address lists.

---

## 1. Snapshot (2026-09-19, before more authorize)

From Singapore, `BatchMode` + the local hub identity:

| Target role | Mesh visible | BatchMode SSH (today) | P0 action |
|---|---|---|---|
| tokyo / rescue | yes | **success** | Re-verify only (already authorized) |
| seoul | yes | Permission denied (pubkey not authorized) | Authorize after Q1 `go` |
| bangkok-mini | yes | Permission denied (pubkey not authorized) | Authorize after Q1 `go` |
| Singapore-loop | self | Permission denied (pubkey not authorized) | Skip unless you want localhost SSH |
| Air | yes | not a hub target | Laptop; not a peer to “fix” |
| Pro | offline / timeout | timed out | Skip unless Q3 `go` |

`Permission denied (publickey)` means: the hub **public** key is not in that user’s `authorized_keys` (or a different user/key is in play). It does **not** mean “host is down.”

---

## 2. On Singapore — identify the hub public key

Use the existing hub identity unless owner `go` on Q2 says “generate a dedicated key first.”

```bash
# On Singapore, as the hub user. Public half only.
ssh-add -L 2>/dev/null | head
# or
test -f ~/.ssh/id_ed25519.pub && echo "pub file present"
# print to the terminal you are sitting at — do not redirect into git
```

If Q2 is **dedicated key**:

```bash
# Still on Singapore. Comment is a role label, not a secret.
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519_sg_hub -C "fleet-singapore-hub" -N ""
# Then use -i ~/.ssh/id_ed25519_sg_hub for tests below.
```

Do not generate keys on the Eden VM. Do not invent a passphrase here and write it down in this file.

Optional SSH config **on Singapore only** (role aliases, no addresses in git):

```
# ~/.ssh/config  — fill HostName from the mesh CLI on that machine, not from this doc
Host fleet-tokyo
  User <existing-user-on-tokyo>
  IdentityFile ~/.ssh/id_ed25519
  IdentitiesOnly yes
  BatchMode yes
```

Repeat `Host` stanzas for `fleet-seoul` and `fleet-bangkok-mini` the same way. Keep that file local.

---

## 3. Authorize the public key on each peer

You need an **existing** login to the peer (owner password/key, tokyo rescue path, or physical/console). Singapore cannot push its own pubkey to a box that already refuses it.

On the **peer**, as the intended SSH user:

```bash
umask 077
mkdir -p ~/.ssh
chmod 700 ~/.ssh
# Append ONE line: the Singapore hub public key you printed in §2.
# Use a local editor or a here-doc you type yourself. Do not curl from a gist.
touch ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

Then, **from Singapore**:

```bash
ssh -o BatchMode=yes -o ConnectTimeout=8 -o IdentitiesOnly=yes \
  -i ~/.ssh/id_ed25519 \
  <existing-user>@<mesh-name-of-peer> true
echo $?
```

| Exit | Meaning | Next |
|---|---|---|
| `0` | Authorized | Mark role `authorized` |
| `255` + `Permission denied (publickey)` | Still not this pubkey / this user | Check user, file mode, which pub line you appended |
| timeout / no route | Mesh or host down | Do not “fix” by opening a public port from this doc |

**Order after Q1 `go`:** seoul, then bangkok-mini, then re-check tokyo. Pro only if Q3 `go` **and** the host is reachable.

**bangkok-mini note:** SSH as the existing user can work while GUI / sudo password is still a separate owner item. Do not treat a sudo deadlock as a pubkey failure.

**Do not** from Singapore:

```bash
# reject: copying private keys around
scp ~/.ssh/id_ed25519 peer:~/.ssh/
# reject: ssh-copy-id if it would require pasting a password into an agent log
```

`ssh-copy-id` is acceptable only when **you** are at an interactive owner session and you understand the password is not being captured into a transcript you will publish.

---

## 4. Signal path (verify, do not dump)

Signal already lives on the execution plane (Singapore). The question is health, not a new install.

From a seat that **already** reaches Singapore:

```bash
# Role-level checks. Stop if a command prints tokens or full device lists you
# would be tempted to paste into git.
systemctl --user is-active signal-agent.service 2>/dev/null || true
# If the project helper exists:
signal-agent whoami
```

Pass bar (write these as words, not payloads):

- [ ] `whoami` succeeds (linked device includes the Singapore role)
- [ ] A **receive** envelope newer than your freshness threshold exists (same-day Hub alarms have said “no receive envelope for N minutes” — treat as recurring, not as a secret)
- [ ] Send remains owner-gated; this checklist does **not** send mail or Signal

Fail bar:

- Do not paste `whoami` JSON, phone numbers, group names, or message bodies into this repo or a public PR.
- Do not “repair” Signal by moving its store onto the Eden VM.

If receive is stale: file a Hub receipt (`role=fleet-singapore`, `signal=stale`, no dumps) and leave a Mac/Adam packet. Do not page the owner with logs.

---

## 5. Acceptance (P0)

All of the following, with **role names only** in the receipt:

- [ ] tokyo/rescue: `BatchMode` still `0` (no regression)
- [ ] seoul: `BatchMode` `0` **or** owner `no-go` on Q1
- [ ] bangkok-mini: `BatchMode` `0` **or** owner `no-go` on Q1
- [ ] Pro: skipped or `0` per Q3
- [ ] Singapore-loop: ignored or optionally `0`
- [ ] Signal: §4 pass or a dated stale-receipt
- [ ] Eden VM: still has **no** new fleet private key and **no** new mesh client
- [ ] This repo / PR: still contains **no** pubkey lines, IPs, or `authorized_keys` excerpts

Hub receipt shape (content, not a template to fill with secrets):

```
singapore-hub mesh P0
date: YYYY-MM-DD
tokyo: ok
seoul: ok | denied | skipped
bangkok-mini: ok | denied | skipped
pro: skipped | ok | timeout
signal: green | stale
eden-vm-keys: none
```

---

## 6. Rollback

- On a peer: delete the **one** Singapore hub line from that user’s `authorized_keys`. Do not wipe the whole file.
- If the private half ever left Singapore: generate a new hub key (Q2 path), authorize the new public half, remove the old line on every role that had it.
- Computers jump is unrelated: disabling Grok Bot / linger does not revoke SSH, and removing a pubkey does not stop Eden local-exec on Singapore itself.
