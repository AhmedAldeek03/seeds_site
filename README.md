# Seeds site

A ready-to-use Seeds site for organisations. It builds on
[Seeds template](https://github.com/AhmedAldeek03/seeds_template) and adds what site owners and
editors need on day one: a home page, a Media center with News and Events, a Contact us page,
demo content, an editorial workflow, ready-made roles and cookie consent.

Use **Seeds template** for a lean starting point that developers build on. Use **Seeds site**
when the people running the site should be able to start right away.

## What it installs

### Recipes

| Recipe | Why |
|---|---|
| [Seeds template](https://github.com/AhmedAldeek03/seeds_template) | The Seeds foundation (Seeds base) and every Seeds feature recipe, ready in *Extend > Browse*. |
| [Media center (Seeds)](https://github.com/AhmedAldeek03/media_center_seeds) | News and Events. |
| [Contact form](https://github.com/AhmedAldeek03/contact_form_recipe) | The Contact us page (Webform). |
| Easy Email Express | HTML versions of every core email. |
| Basic block type (core) | The block type used for the Getting started box. |
| Administrator role (core) | An Administrator role with every permission. |

### Modules and themes

These come on top of what Seeds template already installs.

| Purpose | Modules |
|---|---|
| Look | Seeds site theme (default front-end theme) |
| Dashboards and login redirect | Dashboard, ECA (`eca`, `eca_base`, `eca_user`) |
| Editorial workflow | Content Moderation, Workflows, Scheduler Content Moderation Integration |
| Cookie consent | Klaro |
| Accessibility checker | Editoria11y |
| Site search | Search API, Search API Database |
| Audit log | Admin Audit Trail, with its Auth, Media, Menu, Node, Taxonomy and User sub-modules |
| Visual pages | Canvas, Block |
| Menus, page addresses and redirects | Menu UI, Menu link content, Pathauto, Redirect |
| Lists and bulk actions | Views, Views UI, Views Bulk Operations |

### Modules that come from Seeds template

Seeds site doesn't install these itself; they come with
[Seeds template](https://github.com/AhmedAldeek03/seeds_template). Some are installed but not yet
switched on for anything, as the last column shows.

**Editor helpers**

| Module | What it does | On a fresh Seeds site |
|---|---|---|
| Autosave Form | Saves the edit form every minute, and offers to restore it after a crash or reload. | Works |
| SAM (Simple Add More) | Shows one empty row for fields that take several values, with an *Add another item* button, instead of many empty rows. | Works |
| Login with email or username | People can log in with either. | Works |
| Media File Delete | Deleting a media item also deletes its file. | Works |
| Media Library Edit | Edit a media item from inside the media library. | Works |
| Length Indicator | Shows how many characters are left. | Works on the title, SEO title and SEO description of News and Events |
| Tagify | Tag-style autocomplete with pills. | Installed; no field uses it (Tags use a select list) |
| Media Library Bulk Upload | Upload many images at once. | Installed; no media type is set up for it |
| SVG Image | Lets image fields accept SVG files. | Installed; Image media doesn't allow `.svg` |
| Scheduler | Publish or unpublish content at a set date. | Installed; not enabled on News or Events |

**SEO**: Seeds SEO, Metatag (with Open Graph), Yoast SEO, Simple XML Sitemap, Redirect, Easy
Breadcrumb, Responsive Image Preload.

**Site building and admin**: Seeds Layouts, Seeds Administration, the ECA Modeler and the other
ECA sub-modules, Project Browser and Package Manager (*Add features*), Field UI, Token OR,
Config Language Lock.

Seeds template itself builds on [Seeds base](https://github.com/AhmedAldeek03/seeds_base), which
adds the foundation: the Seeds UI theme, the Seeds editor, media and toolbar modules, CKEditor
plugins, security (Password Policy, Email TFA, SecKit, Restrict IP, Session Limit, CAPTCHA and
reCAPTCHA) and performance modules.

## What you get

### Pages and menus

| Page | Address | Built with |
|---|---|---|
| Home | `/` (alias `/home`) | Canvas page: hero, highlights, latest news, upcoming events, call to action |
| Media center | `/media-center` | Canvas page: latest news, upcoming events, links to all news and events |
| News | `/media-center/news` | View `seeds_site_news` |
| Events | `/media-center/events` | View `seeds_site_events` (upcoming only) |
| Contact us | `/contact-us` | Webform from the Contact form recipe |
| Search | `/search` | Search API with a database server |

Header menu: **Home**, **Media center** (News, Events), **Contact us**. *Media center* is a
link to its own page, and its dropdown opens on hover. Footer menu: News,
Events, Search, Contact us.

### Demo content

Three News items, three Events, six images and three tags, all created by the blocked
`demo_content` user. Remove them in one go at **Content > Demo content** and
**Content > Demo media** (select all, *Delete*). The home page and the menus stay.

### For editors

| Feature | Details |
|---|---|
| Editorial workflow | *Seeds editorial*: Draft → In review → Published, and Archived. Applies to News and Events. Scheduler Content Moderation Integration is installed, but Scheduler is not enabled on News or Events yet. |
| Roles | **Editor** (`content_editor`) writes drafts and submits them for review. **Administrator** has every permission, and reviews and publishes content (core's Administrator role recipe). |
| Dashboards | **Admin dashboard** (`/admin/dashboard/admin`): Getting started steps, content waiting for review, recent content, site status and new users. **Editor dashboard** (`/admin/dashboard/editor`): the editor's drafts, content waiting for review, quick links and content they edited recently. |
| Login redirect | The ECA model *Seeds site: open the right dashboard after login* sends people to their dashboard. Anyone who can view the Admin dashboard (Administrators) goes there, even if they also have the Editor role. Editors go to the Editor dashboard. A login link with its own `?destination=` and password-reset links are left alone. |
| Sidebar | *Add features*, *Content*, *Automation* (ECA) and *People* on the first level. Editable at Configuration > User interface > Seeds Toolbar. |
| Visual pages | Canvas, with three Seeds site components (Hero, Highlights, Call to action) plus the Seeds UI components and the News and Events blocks. |
| Accessibility checker | Editoria11y highlights issues while editing. |
| Help text | Short tips on the page URL, summary, SEO and date fields. |
| HTML emails | Easy Email Express replaces every core email with an HTML version. |
| Audit log | Admin Audit Trail logs changes to content, media, menus, terms, users and logins. |

### For visitors

| Feature | Details |
|---|---|
| Cookie consent | Klaro shows a notice on the first visit and a button to change the choice later. It is off on `/admin` and `/canvas`. Replace it with the Seeds solution once that is ready. |
| Site styles | The [Seeds site theme](https://github.com/AhmedAldeek03/seeds_site_theme), a Seeds UI subtheme, is the front-end theme. It adds a light stylesheet (header, menu, cards, forms, footer) and keeps parent menu items like *Media center* clickable. Change the look in the theme's `css/site.css`. |
| No author lines | News and Events don't show "By author, date". |

## Install

The project needs the same Composer setup as Seeds template (the Seeds recipes come from
GitHub), plus this repository:

```bash
composer config repositories.seeds_site '{"type":"vcs","url":"https://github.com/AhmedAldeek03/seeds_site","no-api":true}'
composer config repositories.seeds_site_theme '{"type":"vcs","url":"https://github.com/AhmedAldeek03/seeds_site_theme","no-api":true}'
composer require drupal/seeds_site:1.0.x-dev
```

Then, as for Seeds template, allow Package Manager in `settings.php`:

```php
$settings['testing_package_manager'] = TRUE;
```

And install:

```bash
drush site:install ../recipes/seeds_site --account-name=admin --site-name="My site"
drush search-api:index
```

### Required patches

This repository ships one fix in `patches/`: `restrict_ip` 5.0.1 (from Seeds base) breaks every
page once Canvas is enabled, because it type-hints the concrete `Messenger` class.

Add it to the project's `composer.json` with
[Composer Patches](https://github.com/cweagans/composer-patches) 2:

```json
"extra": {
    "composer-patches": {
        "disable-resolvers": ["\\cweagans\\Composer\\Resolver\\Dependencies"]
    },
    "patches": {
        "drupal/restrict_ip": {
            "Type-hint MessengerInterface so it works with Drupal Canvas": "recipes/seeds_site/patches/restrict_ip-messenger-interface.patch"
        }
    }
}
```

The `disable-resolvers` line stops Composer Patches from applying patches listed by
dependencies; one of them (for Yoast SEO) no longer applies.

## Known issues

- **Trash is not included yet.** Trash replaces the `entity_type.manager` service, and
  `seeds_layouts` type-hints the concrete `EntityTypeManager` class, so the site crashes on
  install. Once `SeedsLayoutsManager::__construct()` takes `EntityTypeManagerInterface`, add
  `trash` back.
- **The header has no search box.** Search is linked from the footer.

## Dashboards and login redirect

Who sees which dashboard is a permission: *Access to Admin dashboard* (`view admin dashboard`) and *Access to Editor dashboard* (`view editor dashboard`). To send another role to a dashboard, give it that permission; the ECA model checks permissions, not role names, so it needs no change. Admins can edit the dashboards at **Structure > Dashboard** and the redirect at **Automation**.

The Dashboard module also opens `/admin/dashboard` after login and shows the first dashboard (by weight) the person can view. The Admin dashboard has the lower weight, so the sidebar's *Dashboard* link and the ECA redirect agree.

## Development

### Demo content

The demo content in `content/` was exported with `drush content:export`. To change it, install a
site from this recipe, edit the content, and export again:

```bash
drush content:export node --with-dependencies --dir=../recipes/seeds_site/content
drush content:export canvas_page --with-dependencies --dir=../recipes/seeds_site/content
drush content:export menu_link_content --with-dependencies --dir=../recipes/seeds_site/content
drush content:export block_content --with-dependencies --dir=../recipes/seeds_site/content
```

Image media must fill both `field_image` (the Seeds source field) and `field_media_image`
(required by core's Image media type).
