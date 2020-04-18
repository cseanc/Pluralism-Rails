# Deploy Jekyll to Heroku

Reference:

- [Official docs](https://blog.heroku.com/jekyll-on-heroku)
- [Blog post](https://emmanuelhayford.com/how-to-deploy-jekyll-to-heroku/) by Emmanuel Hayford

1. Get [Heroku Toolbelt](https://gorails.com/setup)

2. Create new app on Heroku. On Jekyll project root, open Terminal and enter:

   ```bash
   heroku create <custom_app_name>
   ```

3. On project root, create a file `static.json` for Heroku's static buildpack:

   ```json
   {
     "clean_urls": true,
     "https_only": true,
     "root": "_site/"
   }
   ```

4. On project root, create a file `Rakefile` for Heroku's ruby buildpack:

   ```ruby
   task "assets:precompile" do
     exec("jekyll build")
   end
   ```

5. At the end of existing `Gemfile` on project root, add:

   ```ruby
   gem "rake"
   ruby "<project_ruby_version>"
   ```

6. On project root, create a file `Procfile` to specify which command to run on Heroku dyno:

   ```procfile
   web: jekyll serve -P $PORT --no-watch --host 0.0.0.0
   ```

   > The official docs does not mention this step. This step is pointed out by Emmanuel Hayford's blog post link above.

7. Commit changes. `git add --all && git commit -m "<commit_message>"`

8. Push to Heroku

   ```bash
   git push heroku master
   ```

9. If you get `No web processes running` error while opening your site, open Terminal on your project root and enter:

   ```bash
   heroku ps:scale web=1
   ```

   > For more info, see [Scaling Your Dyno](https://devcenter.heroku.com/articles/scaling)

