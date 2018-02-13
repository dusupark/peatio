Adding a new cryptocurrency

### Cryptocurrencies

name      key         code
----      ---         ----
Bitcoin   satoshi     btc
Ethereum  wei         eth
Ripple    drop        xrp
Qtum      qtumsatoshi qtum

**1. Create or edit the following files:
app/
  assets/
    javascrpts/
      funds/
        models/
          withdraw.js.coffee
    controllers/
      admin/
          deposits/
            {key}s_controller.rb
          withdraws/
            {key}s_controller.rb
        private/
          deposits/
            {key}s_controller.rb
          withdraws/
            {key}s_controller.rb 
          assets_controller.rb
        models/
          admin/
            ability.rb
          deposits/
            {key}.rb
          withdraws/
            {key}.rb
        services/
          coin_rpc.rb
        views/
          admin/
            deposits/
              {key}s/
                index.html.slim
            withdraws/
              {key}s/
                _table.html.slim
                index.html.slim
                show.html.slim
            private/
              assets/
                _{code}_assets.html.slim
                _liability_tabs.html.slim
                index.html.slim
              withdraws/
                {key}s/
                  edit.html.slim
                  new.html.slim
config/
  locales/
    client.en.yml
    client.ko.yml
    client.zh-CN.yml
    server.en.yml
    server.ko.yml
    server.zh-CN.yml
  currencies.yml
  deposit_channels.yml
  markets.yml
  withdraw_channels.yml
public/
  templates/
    funds/
      deposit.html
      deposit_{code}.html
      withdraw.html
      withdraw_{code}.html
  icon-{code}.png

**2. Run assets:clobber and assets:precompile.

~/peatio/current$ bundle exec rake assets:clobber
~/peatio/current$ bundle exec rake assets:precompile

**3. Run migration:accounts.

~/peatio/current$ bundle exec rake migration:accounts

**4. Run solvency:liability_proof.

~/peatio/current$ bundle exec rake solvency:liability_proof

**5. Restart daemons.

~/peatio/current$ bundle exec rake daemons:stop
~/peatio/current$ rm -f log/*
~/peatio/current$ bundle exec rake daemons:start

**6. Restart nginx.

~/peatio/current$ sudo service nginx restart
