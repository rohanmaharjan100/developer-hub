---
title: "Mobile and web SDK: Does the SDK cache expire?"
sidebar_label: "Mobile and web SDK: Does the SDK cache expire?"
sidebar_position: 8
---

<p>
  <button hidden style={{borderRadius:'8px', border:'1px', fontFamily:'Courier New', fontWeight:'800', textAlign:'left'}}> help.split.io link: https://help.split.io/hc/en-us/articles/360058277992-Mobile-and-web-SDK-Does-the-SDK-cache-expire </button>
</p>

## Question

The Split mobile (iOS and Android) and JavaScript Browser SDKs download a local cache and store it in a file system. Does the cache have an expire date or TTL?

## Answer

The SDK will consider the cache stale if it hasn't been updated for 90 days. In such case it will issue a full download of FME definitions. This is an unlikely scenario since the SDK is continuously synching changes from the Harness FME servers and updating the cache.