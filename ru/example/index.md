---
title: 'Example'
draft: 1
---

## chart

{{< chart 90 200 >}}
{
    type: 'bar',
    data: {
        labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
        datasets: [{
            label: 'Bar Chart',
            data: [12, 19, 18, 16, 13, 14],
            backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
            ],
            borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
            ],
            borderWidth: 1
        }]
    },
    options: {
        maintainAspectRatio: false,
        scales: {
            yAxes: [{
                ticks: {
                    beginAtZero: true
                }
            }]
        }
    }
}
{{< /chart >}}

---

{{< chart 90 200 >}}
{
    type: 'radar',
    data: {
        labels: [
'Eating',
'Drinking',
'Sleeping',
'Designing',
'Coding',
'Cycling',
'Running'
],
        datasets: [{
label: 'My First Dataset',
data: [65, 59, 90, 81, 56, 55, 40],
fill: true,
backgroundColor: 'rgba(255, 99, 132, 0.2)',
borderColor: 'rgb(255, 99, 132)',
pointBackgroundColor: 'rgb(255, 99, 132)',
pointBorderColor: '#fff',
pointHoverBackgroundColor: '#fff',
pointHoverBorderColor: 'rgb(255, 99, 132)'
}, {
label: 'My Second Dataset',
data: [28, 48, 40, 19, 96, 27, 100],
fill: true,
backgroundColor: 'rgba(54, 162, 235, 0.2)',
borderColor: 'rgb(54, 162, 235)',
pointBackgroundColor: 'rgb(54, 162, 235)',
pointBorderColor: '#fff',
pointHoverBackgroundColor: '#fff',
pointHoverBorderColor: 'rgb(54, 162, 235)'
}]
    }
}
{{< /chart >}}

---

## url

[example](/example.com)

---

## img

![Alt](https://i.imgur.com/Bnvurtb.jpg)

---

## gist

{{< gist "KitsuneSolar" "38ec420079c1d86443012fa44a22be7f" >}}

{{< gist spf13 7896402 "img.html" >}}

---

## uuid-url

{{< uuid "16cabd8a-e624-5911-904d-9d9da85e0bce" >}}

---

## imgur

{{< imgur id="prFvxmE.jpeg" >}}

{{< imgur id="Yhim15t.jpg" >}}

---

## diagram

{{< diagram >}}
classDiagram
Class01 <|-- AveryLongClass : Cool
Class03 *-- Class04
Class05 o-- Class06
Class07 .. Class08
Class09 --> C2 : Where am i?
Class09 --* C3
Class09 --|> Class07
Class07 : equals()
Class07 : Object[] elementData
Class01 : size()
Class01 : int chimp
Class01 : int gorilla
Class08 <--> C2: Cool label
{{< /diagram >}}

---

{{< diagram >}}
sequenceDiagram
    participant Alice
    participant Bob
    Alice->>John: Hello John, how are you?
    loop Healthcheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts <br/>prevail!
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Jolly good!
{{< /diagram >}}

---

## map

{{< map lat="51.505" lon="-0.09" zoom="13" >}}

---

{{< map lat="52.505" lon="-0.09" zoom="13" >}}

---

## form-search

{{< form-search "qwee" >}}

---

## carousel

{{< carousel "https://i.imgur.com/2ji2e1W.jpg|https://i.imgur.com/9amQBlk.jpg" >}}

---

## vk-users

{{< vk-users "109195958|197594655|37261902" >}}

---

## github-users

{{< github-users "KitsuneSolar|davidsneighbour|a8m|zeke" >}}

---

## github-users-repos

{{< github-users-repos "KitsuneSolar" >}}

---

## github-users-orgs

{{< github-users-orgs "KitsuneSolar|davidsneighbour" >}}

---

## github-orgs

{{< github-orgs "themefisher|GitHub|marketplace-hugo" >}}

---

## github-repos

{{< github-repos "marketplace-flarum/flarum-l10n-core-russian|marketplace-hugo/hugo-ext-shortcodes|marketplace-xenforo/xenforo-ext-thread-starter" >}}

---

{{< requisites "https://raw.githubusercontent.com/KitsuneSolar/KitsuneSolar/main/requisites.json" "organization" >}}

{{< requisites "https://raw.githubusercontent.com/KitsuneSolar/KitsuneSolar/main/requisites.json" "bank-account" >}}

---

{{< progress "60" "success" >}}

---

{{< mention "KitsuneSolar" >}}

---

{{< abbr "HTML" "HyperText Markup Language" >}}

---

{{< form-contact subject="" token="73e8bec2-2f2a-4062-8f01-c6579cfe7836" >}}

---

{{< form-donate
wallet="410012478387285"
paypal="qw"
patreon="qw"
liberapay="qw"
ko-fi="qw"
buymeacoffee="qw"
usd="4584 4328 1371 3790"
eur="4584 4328 1893 8194"
rub="4584 4328 1325 5511"
btc="bc1q855dt7p8mtd74yw96vvu93wy59j0fl8gaqh62h"
eth="0x7252D91B61E18eDE4c8ec43a0EE7F1dFD17542ab"
xmr="48Q1zEztoECNyijSoQVhHC12LaxzNLPrhBgwGdM2847QY8ayusQ6XBjCD9hgeQk2LLUKbBvC5yKxDDmzkGvGyMGE9o95YkR" >}}