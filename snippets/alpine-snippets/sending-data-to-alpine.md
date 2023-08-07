---
title: Sending data to alpinejs
published_at: 2023-08-07
updated_at: 2023-08-07T13:34:30.015Z
---

# sending-data-to-alpine
#alpinejs #laravel #php #javascript #snippet

In order to send data from laravel backend to alpinejs, we can use the following code:

```javascript
x-data="{
    showLikePopover: false,
    showDislikePopover: false,
    likeStatus: {{ auth()->user()?->likesComments->where('comment_id', $comment->id)->first()->like_status ?? 0}} ?? 0, // [!code hl]
    }"
```

We are using the mustache syntax to send data from laravel backend to alpinejs.
