---
canvasWidth: 700
layout: cover
theme: dracula
text-align: center
title: 200 Domains on one Magento Instance with $300 Hosting Bill
---

# 200 Domains

# 1 Magento Instance 

# $300 Hosting Bill

---

# About me

<v-clicks>

👨‍💻 18+ years of Magento Development Experience

🚀 Expert in optimizing everything

🧯 Putting out fires on production

❤️ Passionate about Open Source

</v-clicks>

---
layout: fact
---

# 10 years ago...

---
layout: image-left
image: ./coolblue.png
imageColClass: ml-0 my-0 bg-center
---

# I want like Coolblue.nl
<v-clicks>

🥉 🇳🇱 2024 (Amazon #4)

2014: 💶360M

2023: 💶2.4B

437 👩‍💻 / 5.7K 👥

[Screenshot from 2014](https://web.archive.org/web/20141001045228/http://www.coolblue.nl/ons-assortiment)

</v-clicks>

---
layout: image-left
image: ./hosting.png
imageColClass: ml-0 my-0 bg-center
---

# But Hosting...

<v-clicks>

<Arrow x1="250" y1="300" x2="140" y2="330" color="red" />

🖥 4 CPUs

💾 8GB RAM

🗄 70GB SSD

[Screenshot from 2016](https://web.archive.org/web/20160324062025/https://www.byte.nl/hosting/magento/prijzen)

</v-clicks>

---

# Requirements

<v-clicks>

- Each domain has own category structure 
- Products can be shared between domains.

  E.g. `laptops-for-study.com` and `laptops-for-home.com` 

- Each domain should have unique home-page and logo
- Shared Shopping Cart

</v-clicks>

---
layout: fact
---

# The Magento Way ™

---

![The Magento Way ™](/magento-way.svg)

---

# Major Drawbacks

<v-clicks>

- Index table size < 2.2.x
- Number of index tables >= 2.2.x
- Extra long indexation time 
- MySQL memory buffer usage
- Unnecessary data duplication

</v-clicks>

---

# DevOps Nightmare

```nginx {all|4-12|1-2}
map_hash_max_size ??; # affects runtime performance
map_hash_bucket_size ??; # affects runtime performance

map $http_host $mage_run_code {
    hostnames;
    default           "base"; 
    laptops-for-study.com  "laptops-for-study";
    www.laptops-for-study.com  "laptops-for-study";
    laptops-for-home.com  "laptops-for-home";
    www.laptops-for-home.com  "laptops-for-home";
    # ...
}
# ... 
fastcgi_param  MAGE_RUN_CODE    $mage_run_code;
fastcgi_param  MAGE_RUN_TYPE    "website";
```

---
layout: fact
---

# Let's step back for a second

---

# Ask yourself

<v-clicks>

- Do we need multiple websites?
- Do we need multiple store groups?
- Do we need multiple store views?

</v-clicks>

---
layout: fact
---

# 💡
# A better way 

---

![A better way](/better-way.svg)


---

![A better way](/better-way-with-domains.svg)

---

![A better way](/better-way-domains-anatomy.svg)


---

# Why Better?

<v-clicks>

- Category trees can be shared
- No duplication of index data
- Smaller MySQL database size
- Instant domain addition
- Easier to manage products

</v-clicks>

---
layout: fact
---

# Boring Staff

--- 

# Customizations

<v-clicks>

`Magento\Store\App\FrontController\Plugin\RequestPreprocessor`
Added around plugin that has higher precedence then request processor to preload domain and its configuration. 

`Magento\Store\Api\Data\GroupInterface::getRootCategoryId()`
Added after plugin for frontend scope only to replace with value form domain scope.

`Magento\Framework\App\Config\ScopeConfigInterface::getValue()`
Added after plugin to override values from domain scope

</v-clicks>

---

# Customizations

<v-clicks>

`Magento\Catalog\Plugin\Block\Topmenu::getCategoryTree()`
Added preference to load more efficiently menu and with custom path structure

`Magento\Framework\Search\AdapterInterface::query()`
Added before plugin to modify ES query to include new virtual root and possible additional filters.


</v-clicks>


---

# Customizations

<v-clicks>

`Magento\UrlRewrite\Model\UrlFinderInterface::findOneByData()`
Added before plugin to trim request path of virtual root category

`Magento\Catalog\Model\Category::getUrl()`                                                  
Added after plugin to strip virtual category root prefix from rendering on the frontend url

</v-clicks>

---
layout: fact
---

# Demo Time

---
layout: fact
---
# Thank You!

Access slides here:

[slides.ecom.dev/mm25fl](https://slides.ecom.dev/mm25fl)

Need Help?
[ivan@ecom.dev](mailto:ivan@ecom.dev)
