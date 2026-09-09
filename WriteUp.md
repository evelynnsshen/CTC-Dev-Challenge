# Write-up

> This is the skeleton - replace everything in blockquotes with your own words
> and delete the prompts as you go. Aim for **~300 words** across the four
> questions; the route reference below can be as long as it needs to be.
>
> Write it like you're handing the work to a teammate. We'd rather read an
> honest "I ran out of time on X and here's what I'd do" than a polished list of
> accomplishments. **Submit this even if you didn't finish** - see CHALLENGE.md.

## 1. What did you build for Part B, and why that?

> Although I haven't started implementing my feature for Part B yet, I plan on adding spending summaries to each restaurant that display the total amount spent, total number of visits, and average amount spent per visit. I chose this feature because the app is meant to track how much Brennen spends eating out, but the current UI does not show any of that information. This way, you can easily see which restaurants Brennen visits the most and where he spends the most money.

## 2. What did you decide, and what did you rule out?

> Route shapes, data model, where the logic lives, what you deliberately didn't
> do. Name a tradeoff you're not sure you got right.

## 3. Where did you cut corners?

> What would you fix first with another day?

---

## Part B: routes

> Every endpoint you added, with its request and response shapes, so we can
> exercise it without reverse-engineering your code. Add or remove rows as
> needed; delete this section if your Part B added no routes.

| Method and path | What it does | Success | Errors       |
| --------------- | ------------ | ------- | ------------ |
| `GET /api/...`  |              | `200` + | `404` if ... |
| `POST /api/...` |              | `201` + | `400` on ... |

**`POST /api/...`**

```jsonc
// request
{ }

// 201 response
{ }
```

## Schema changes

> Any migrations you added (`002_*.sql`, ...), new tables or columns, and
> anything a reviewer needs to run beyond `./setup.sh`. Write "none" if there
> were none.

## How I verified this

> How you checked your work - the happy paths _and_ the failures. `curl`
> commands, a Postman collection, a scratch script, screenshots: whatever you
> actually used. Paste the commands.
>
> This is much faster for us to review than working it out ourselves, and it's
> how you show you checked the edge cases.

**Part A** - the contract table in CHALLENGE.md, every row including the error
cases:

```bash
# e.g.
curl -i http://localhost:3000/api/restaurants          # 200 + array
# HTTP/1.1 200 OK
# vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch
# content-type: application/json
# Date: Wed, 09 Sep 2026 21:43:27 GMT
# Connection: keep-alive
# Keep-Alive: timeout=5
# Transfer-Encoding: chunked

# [{"id":6,"name":"Valid Spot","cuisine":"Test","address":"2 Test St","rating":4.5,"created_at":"2026-09-09T21:32:37.742Z"},{"id":1,"name":"The Rusty Spoon","cuisine":"American","address":"12 Main St","rating":4.5,"created_at":"2026-09-09T08:21:31.166Z"},{"id":2,"name":"Sakura House","cuisine":"Japanese","address":"88 Cherry Ln","rating":4.8,"created_at":"2026-09-09T08:21:31.166Z"},{"id":3,"name":"Bella Napoli","cuisine":"Italian","address":"301 Olive Ave","rating":4.2,"created_at":"2026-09-09T08:21:31.166Z"},{"id":4,"name":"El Fuego","cuisine":"Mexican","address":"47 Sol Blvd","rating":4.6,"created_at":"2026-09-09T08:21:31.166Z"},{"id":5,"name":"Green Bowl","cuisine":"Vegetarian","address":"5 Garden Way","rating":3.9,"created_at":"2026-09-09T08:21:31.166Z"}]%
curl -i http://localhost:3000/api/restaurants/99999    # 404
# HTTP/1.1 404 Not Found
# vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch
# content-type: application/json
# Date: Wed, 09 Sep 2026 21:45:46 GMT
# Connection: keep-alive
# Keep-Alive: timeout=5
# Transfer-Encoding: chunked

# {"error":"Restaurant not found"}%    
curl -i http://localhost:3000/api/restaurants/abc      # 404
# HTTP/1.1 404 Not Found
# vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch
# content-type: application/json
# Date: Wed, 09 Sep 2026 21:46:01 GMT
# Connection: keep-alive
# Keep-Alive: timeout=5
# Transfer-Encoding: chunked

# {"error":"Restaurant not found"}%     
curl -i -X POST http://localhost:3000/api/restaurants \
  -H 'Content-Type: application/json' \
  -d '{"name":"Out Of Range","rating":6}'              # 400
# HTTP/1.1 400 Bad Request
# vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch
# content-type: application/json
# Date: Wed, 09 Sep 2026 21:46:30 GMT
# Connection: keep-alive
# Keep-Alive: timeout=5
# Transfer-Encoding: chunked

# {"error":"Invalid restaurant data"}% 
```

**Part B** - the equivalent cases for what you built:

```bash

```

## Known issues / what I'd do next

> Anything broken, unfinished, or that you know is wrong. Being upfront here
> costs you nothing and tells us a lot.

> The database uses ON DELETE CASCADE, so deleting a restaurant also deletes all visits associated with it. I agree with this behavior because visits should not remain if their restaurant no longer exists.