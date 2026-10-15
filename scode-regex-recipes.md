# ⚡ VS Code Regex Recipes for CI3 to CI4

Stop doing manual find-and-replace! These Regular Expression (Regex) recipes are designed to be used in **VS Code** to instantly update legacy CodeIgniter 3 syntax to CodeIgniter 4 across your entire project.

### 🛠️ How to use these recipes in VS Code:
1. Open your project in VS Code.
2. Press `Ctrl + H` (Windows/Linux) or `Cmd + Option + F` (Mac) to open the Search and Replace panel.
3. **CRITICAL:** Click the small **`.*`** icon (Use Regular Expression) in the search box to enable Regex mode.
4. Copy the **Find** pattern, paste it in the top box. Copy the **Replace** pattern, paste it in the bottom box.
5. Click "Replace All" (the double arrow icon).

> ⚠️ **Safety First:** Always commit your code to a new Git branch before running Regex replacements across your whole project!

---

## Recipe 1: Upgrading POST Data Retrieval
In CI3, we used `$this->input->post()`. In CI4, this is handled by the Request object.

*   **Find:** `\$this->input->post\('(.*?)'\)`
*   **Replace:** `$this->request->getPost('$1')`
*   **What it does:** Finds all instances of fetching POST data and updates it to the CI4 Request service method.

---

## Recipe 2: Upgrading GET Data Retrieval
Similarly, CI3 used `$this->input->get()`. CI4 uses a specific method for GET variables to prevent confusion with POST.

*   **Find:** `\$this->input->get\('(.*?)'\)`
*   **Replace:** `$this->request->getGet('$1')`
*   **What it does:** Updates GET variable retrieval to CI4's `getGet()` method.

---

## Recipe 3: Fixing the `redirect()` Function
In CI3, `redirect()` just fired. In CI4, it returns a Response object, meaning you must `return` it in your controllers to stop execution.

*   **Find:** `redirect\('(.*?)'\);`
*   **Replace:** `return redirect()->to('$1');`
*   **What it does:** Wraps the old redirect function in the new CI4 RedirectResponse builder and adds the crucial `return` statement.

---

## Recipe 4: Removing Deprecated Library Loads
CI4 automatically loads many core libraries that had to be manually loaded in CI3. We can use Regex to comment these out or remove them.

*   **Find:** `\$this->load->library\('session'\);`
*   **Replace:** `// CI4: Session is loaded automatically. Use service('session') or session() helper.`
*   **What it does:** Finds the old session loader and replaces it with a helpful comment. (You can change `'session'` to `'form_validation'` or `'pagination'` to do the same for those!).

---

## Recipe 5: Updating the Base Controller Extension
Every CI3 controller extends `CI_Controller`. In CI4, it extends `BaseController`.

*   **Find:** `extends CI_Controller`
*   **Replace:** `extends BaseController`
*   **What it does:** A simple but massive time-saver. Updates the parent class for every single controller in your `application/controllers` (now `app/Controllers`) folder.

---

### 💡 Pro Tip for Custom Regex
If you have a custom CI3 helper that you use everywhere (e.g., `my_custom_date_format($date)`), you can write your own regex! 
*   **Find:** `my_custom_date_format\((.*?)\)`
*   **Replace:** `formatDateHelper($1)`

*Have a regex recipe that saves you hours? [Open a Pull Request](./CONTRIBUTING.md) and add it here!*
