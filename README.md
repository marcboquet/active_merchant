# Active Merchant

This project adds integration for Spanish TPVs Sermepa and BBVA to [Active Merchant](https://github.com/Shopify/active_merchant)

It was created using code from [samlown/active_merchant](https://github.com/samlown/active_merchant) and [enriclluelles/active_merchant](https://github.com/enriclluelles/active_merchant)

## Installation

### From Git

You can check out the latest source from git:

    git clone git://github.com/apalancat/active_merchant.git

### As a Rails plugin

ActiveMerchant includes an init.rb file. This means that Rails will automatically load ActiveMerchant on startup. Run
the following command from the root directory of your Rails project to install ActiveMerchant as a Rails plugin:

    script/plugin install git://github.com/apalancat/active_merchant.git

### As a Gem

Add the following to your Gemfile

    gem 'activemerchant', :git => 'git://github.com/apalancat/active_merchant.git'

## Usage

### BBVA

First create an initializer with the commerce info:


	# config/initializers/bbva.rb

	ActiveMerchant::Billing::Integrations::BbvaTpv::Helper.credentials = {
	  :terminal_id   => '999999',
	  :commercial_id => 'X9999999999999',
	  :secret_key    => 'secretkey',
	  :secret_key_data => '99;99;99;99;99;99;99;99;99;99;99;99;99;99;99;99;99;99;99;99'
	}

	# include the view helper in order to be able to generate the form
	require 'active_merchant/billing/integrations/action_view_helper'
	ActionView::Base.send(:include, ActiveMerchant::Billing::Integrations::ActionViewHelper)

Then generate the form in the view:

	
	<%= payment_service_for "123", 'The Shop', :amount => 50000, :currency => 'EUR', :service => :bbva_tpv do |service| %>
	  	<% service.description "Some description of the purchase"%>
	  	<% service.customer_name "Name"%>
	  	<% service.notify_url ""%>
	  	<% service.success_url ""%>
	  	<% service.failure_url ""%>

	  	<%= submit_tag "Go to payment gateway!"%>
  	<%end%>


For further info see @samlown documentation on [integration with Sermepa](https://github.com/samlown/active_merchant_sermepa#active-merchant-sermepa-plugin)

Shopify's [API documentation](http://rubydoc.info/github/Shopify/active_merchant/master/file/README.md).
