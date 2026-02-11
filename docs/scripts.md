---
layout: default
title: scrape_test / sbr_test Scripts
parent: Documentation
nav_order: 5
---

# scrape_test / sbr_test Scripts

`scrape_test` and `sbr_test` are two internal scripts, which are used to stress-test and improve the CAPTCHA solver by mass-collecting image data when SR is low.

---

## **1. scrape_test (The Mass Requester)**

This is a straightforward tool designed to "hammer" a site with requests to trigger CAPTCHA challenges.

**When to Use**: CAPTCHA appears immediately on URL.

1. **Function:** It allows for high-volume automated requests without complex user logic.

2. **Workflow:**

   **Step 1**: Download a list of target URLs (e.g., product pages).

	```bash
	scrape_test urls -l 10000 -d homedepot.com -g pdp --days 1 > homedepot_pdp.txt
	```

	**Step 2**: Use the run command to send requests (e.g., 10 times) to those URLs.

	```bash
	scrape_test run -u './homedepot_pdp.txt' -g scrape_r.js -t -B 'output' --clear -n 10
	```

4. **Best Practice:** It’s recommended to use randomized URLs rather than hitting the same page repeatedly to avoid being blocked by the target site’s server.

5. **CAPTCHA Integration:** If the inhouse_solver rules are configured with the correct Selectors for that site, `scrape_test` will automatically trigger a CAPTCHA solve and save the images to the dashboard.

---

## 2. **sbr_test (The Scenario Solver):**

This is a more functional tool that executes a complex, step-by-step user scenario to reach a CAPTCHA.

**When to Use:** CAPTCHA appears after form/click.

1. **Function:** Unlike the request-only `scrape_test`, this script can fill out forms, click buttons, and navigate deep into a site.
   ```bash
	sbr_test "@chatgpt_view-source.js" --parallel 30 --samples 30
	```

3. **Technology:** It supports various automation frameworks like Puppeteer, Playwright, and Selenium.

4. **Workflow:** It follows a predefined "scenario" file provided by the support or development teams. For example, a script might navigate to a checkout page and only then attempt to solve the CAPTCHA that appears.

   Example for sbr_test scenario:
   ```javascript
    // sbr_test --scenario scenario.js
    module.exports = async (page, {client, sleep, idx}) => {
    await client.send('Unlocker.setRules', {rules: {
        // captcha_solvers: ['deathbycaptcha'],
        captcha_solvers: ['anti_captcha'],
        // captcha_solvers: ['capmonster'],
        hcaptcha_conf: {
            pass_proxy: false,
            submit_form: true,
        },
    }});

    console.log('Navigating...');
	await page.goto('https://iapps.courts.state.ny.us/webcivil/FCASCalendarSearch');
	console.log('Navigated, filling form...');
	await page.waitForSelector('select#cboCourt');
	await page.select('select#cboCourt', '80');
	await page.waitForSelector('select#cboCourtPart');
	await page.select('select#cboCourtPart', '38968');
	console.log('clicking "find calendar" and waiting results');
	await page.locator("input#btnFindCalendar").click();
	await page.waitForNavigation();
    console.log('Waiting captcha to solve...');
    const {status} = await client.send('Captcha.waitForSolve');
    console.log('Captcha solve status:', status);
    try {
        await page.waitForSelector(`a[href*="FCASCalendarDetail"]`, { timeout: 60000 });
        console.log("Search results appeared");
    } finally {
        await page.screenshot({ path: `iapps.courts.state.ny.us2_${idx}_res.png` });
    }
    };

    ```

5. **Debug Mode:** It features a visual Debug Mode that opens a browser window so you can watch the script execute in real-time.
   ```bash
	sbr_test "@chatgpt_view-source.js" --debug
	```
