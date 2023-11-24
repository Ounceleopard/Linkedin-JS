# Linkedin-JS
Unfollow everyone on linkedin with one command

## Steps

1. Visit www.linkedin.com/feed/following.

2. Open Developer Tools in Chrome
Right Click -> Inspect. Switch to the console tab.

3. Run the following code in the console

```bash

(() => {
  let count = 0;
  function getAllButtons() {
    return document.querySelectorAll('button.is-following') || [];
  }
  async function unfollowAll() {
    const buttons = getAllButtons();

    for (let button of buttons) {
      count = count + 1;

      const name = button.parentElement.querySelector(
        '.follows-recommendation-card__name',
      ).innerText;
      console.log(`Unfollow #${count}:`, name);

      window.scrollTo(0, button.offsetTop - 260);
      button.click();

      await new Promise((resolve) => setTimeout(resolve, 100));
    }
  }
  async function run() {
    await unfollowAll();
    window.scrollTo(0, document.body.scrollHeight);
    await new Promise((resolve) => setTimeout(resolve, 1000));
    const buttons = getAllButtons();
    if (buttons.length) run();
  }
  run();
})();

```
