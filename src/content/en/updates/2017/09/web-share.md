project_path: /web/_project.yaml
book_path: /web/updates/_book.yaml
description: Web Share is now available in Chrome 61 for Android.

{# wf_published_on: 2017-09-05 #}
{# wf_updated_on: 2017-09-05 #}
{# wf_featured_image: /web/updates/images/generic/share.png #}
{# wf_tags: chrome61,sharing,android #}
{# wf_featured_snippet: Web Share is now available in Chrome 61 for Android. Use the <code>navigator.share()</code> method to invoke the native sharing capabilities of the host platform. #}

# Web Share API available in Chrome 61 {: .page-title }

{% include "web/_shared/contributors/samthorogood.html" %}

In Chrome 61 for Android, we've launched the `navigator.share()` method, which allows
websites to invoke the native sharing capabilities of the host platform. This method,
part of the [Web Share API](https://wicg.github.io/web-share/), allows you easily trigger
the native Android share dialog, passing either a URL or text to share.

## Usage

The Web Share API is a
[Promise](/web/fundamentals/getting-started/primers/promises)-based, single method API.
It accepts an object which must have at least one of the properties named `text` or
`url`.

```js
if ('share' in navigator) {
  navigator.share({
      title: 'Web Fundamentals',
      text: 'Check out Web Fundamentals—it rocks!,
      url: 'https://developers.google.com/web',
  })
    .then(() => console.log('Successful share'))
    .catch((error) => console.log('Error sharing', error));
}
```

To use the Web Share API:

* you must be served over [HTTPS](https://www.chromium.org/Home/chromium-security/prefer-secure-origins-for-powerful-new-features)

* you should feature-detect it in case it's not available on your users' platform

* you can only invoke the API in response to a user action, such as a click

* you can also share any URL, not just URLs under your website's current scope: and you
  may also share `text` without a URL

## Case Study

[Santa Tracker](https://santatracker.google.com) is a holiday tradition here at
Google. Every December, you can celebrate the season with games and educational
experiences: and in the new year, Santa Tracker [is open-sourced and delivered](https://developers.googleblog.com/2017/04/santa-tracker-open-sourced-and-delivered.html).

In 2016, we used the Web Share API on Android via an
[Origin Trial](https://github.com/jpchase/OriginTrials/blob/gh-pages/developer-guide.md)
(note: this is **not** required to use the Web Share API now, as part of Chrome 61). This
API was a perfect fit for mobile—in previous years, we had disabled share buttons on mobile,
as space is at a premimum and we couldn't justify having several share targets.

<img alt="Santa Tracker share button" src="/web/updates/images/2017/09/santa-phone.png" style="margin: 12px auto;"/>

With the Web Share API, we were able to present just one button, saving precious
pixels. We also found that users shared with Web Share around 20% more than users
without the API enabled.

(If you're on Chrome 61 on Android, head to
[Santa Tracker](https://santatracker.google.com) and see Web Share in action.)

## More Information

Read more about the launch at
[Chrome Platform Status](https://www.chromestatus.com/features/5668769141620736). Here
are some important links:

* [Sample](https://github.com/mgiuca/web-share/blob/master/demos/share.html)
* [Share explainer](https://github.com/WICG/web-share/blob/master/docs/explainer.md)

In the future, websites themselves will be allowed to register themselves as a
"[share receiver](https://www.chromestatus.com/features/5662315307335680)", enabling
sharing _to_ the web—from both the web and native apps.

{% include "comment-widget.html" %}
