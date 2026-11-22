Points from the IP evaluation:
Good:
- Use many sources to test the same information so we cross-check it
- Specify used tools used and their version

Bad:
- Use `ipcalc` to identify the correct prefix. Try calculating IP address from the ranges
- Use evidence when recommending to block some IP addresses. We cannot block a whole network without proof.
- Country of origin is not the attacker's location.
- When doing neighboring IP addresses investigation, we need to also check the neighboring addresses.
- We cannot draw conclusions without gathering evidence. For example, seeing that an IP has many reports doesn't mean that it's abusive. We need to explicitly state "by the information provided by this source, this IP appears abusive".
- Avoid statements like "this is a hacker address", because it's just an IP with where the activity comes from. We cannot say that this attacker is from China, because we only know that the activity comes from China
- Cannot say "this IP looks suspicious". Use formal language instead.
- When using AI to query information, be explicit about it: specify sources for AI to look into, specify what we need, etc.
- Need to specify timelines (because IP addresses and ASNs change)
- State not my own conclusions, but instead facts that we observe in databases