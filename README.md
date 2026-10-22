# Seeds site

A ready-to-use Seeds site for organisations. It builds on
[Seeds template](https://github.com/AhmedAldeek03/seeds_template) and adds what site owners and
editors need on day one: a home page, a Media center with News and Events, a Contact us page,
demo content, an editorial workflow, ready-made roles and cookie consent.

Use **Seeds template** for a lean starting point that developers build on. Use **Seeds site**
when the people running the site should be able to start right away.

## What you get

### Pages and menus

| Page | Address | Built with |
|---|---|---|
| Home | `/` (alias `/home`) | Canvas page: hero, highlights, latest news, upcoming events, call to action |
| News | `/media-center/news` | View `seeds_site_news` |
| Events | `/media-center/events` | View `seeds_site_events` (upcoming only) |
| Contact us | `/contact-us` | Webform from the Contact form recipe |
| Search | `/search` | Search API with a database server |

Header menu: **Home**, **Media center** (News, Events), **Contact us**. Footer menu: News,
Events, Search, Contact us.

### Demo content

Three News items, three Events, six images and three tags, all created by the blocked
`demo_content` user. Remove them in one go at **Content > Demo content** and
**Content > Demo media** (select all, *Delete*). The home page and the menus stay.

### For editors

| Feature | Details |
|---|---|
| Editorial workflow | *Seeds editorial*: Draft → In review → Published, and Archived. Applies to News and Events, and works with Scheduler. |
| Roles | **Editor** (`content_editor`) writes drafts and submits them for review. **Reviewer** also publishes and archives. **Site manager** also adds features, manages menus, forms and users, and can give people the Editor and Reviewer roles only (RoleAssign). |
| Welcome dashboard | Getting started steps at the top of the dashboard: site settings, home page, content, features, team, demo content. |
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
| Site styles | Seeds UI is a base theme with almost no CSS. This recipe adds a light stylesheet (header, menu, cards, forms, footer) through Canvas's global CSS (Canvas > Code > Global CSS). Edit it there, or remove it once the site has its own Seeds UI subtheme. The source is `assets/site.css`. |
| No author lines | News and Events don't show "By author, date". |

## Install

The project needs the same Composer setup as Seeds template (the Seeds recipes come from
GitHub), plus this repository:

```bash
composer config repositories.seeds_site '{"type":"vcs","url":"https://github.com/AhmedAldeek03/seeds_site","no-api":true}'
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

### Required patch

`restrict_ip` 5.0.1 (from Seeds base) breaks every page once Canvas is enabled, because it
type-hints the concrete `Messenger` class. This repository ships the fix in `patches/`. Add it
to the project's `composer.json` with
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

## Development

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
