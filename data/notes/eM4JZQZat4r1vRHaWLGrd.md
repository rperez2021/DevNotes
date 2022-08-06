## General Notes

You Are Not the User: The False-Consensus Effect, [Link](https://www.nngroup.com/articles/false-consensus/)

The ` <button> ` element should be used for any interaction that performs an action on the current page. The ` <a> ` element should be used for any interaction that navigates to another view.

Adding an HTML Attribute ` tabindex="0" ` allows tab focus. These can also be numbered to order tabbing.

Synthetic Click Activator

Screen reader users generally use headings to navigate a page quickly. Using heading in orders is super important.

### Cool Examples of All the Things

[A Complete Guide to A11y Components](https://www.smashingmagazine.com/2021/03/complete-guide-accessible-front-end-components/)

### Modals

The final boss battle of a11y! 😂

With Modals make sure that when you close a modal focus is returned to where the modal was opened.

Make sure that the modal is a created just as child of the body, do not nest it far in the document or it will make it harder to navigate.

[WICG Inert Polyfill](https://github.com/WICG/inert) was created to make a DOM Node uninteractable and prevent the user from navigating to that node.

### Contrast Ratio from WCAG 2

Minimum for Text & Images: 4.5:1

Minimum for Large Text: 3:1

Enhanced for Text & Images: 7:1

Enhanced for Large Text: 4:1

#### Tools for Contrast Checking

1. [WCAG Color Contrast Analyzer](https://goo.gl/YVcYIS)

2. [aXe Chrome Extension](https://goo.gl/TMZoBP)

3. [Lea Verous Contrast Ratio](https://goo.gl/0fqfVo)

4. [Automated Testing with aXe](https://goo.gl/Nj31Jj)

### Assistive Tech

1. TalkBack: assistive reader for Mobile Devices.

2. Switch Device: button switch device for low dexterity users.

3. NVDA: Windows Screen Reader

4. VoiceOver: IOS Screen Reader
