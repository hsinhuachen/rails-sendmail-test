# Rails send mail

新增使用者時自動寄信到使用者信箱

## 使用 mailer 這個產生器來建立寄信功能所需要的基本架構

	bin/rails g mailer Contact

## app/mailers/application_mailer.rb
	  class ApplicationMailer < ActionMailer::Base
	    default from: 'from@example.com'
	    layout 'mailer'
	  end

from@example.com 為預設寄件者
layout 為 app/views/layouts/mailer

## app/mailers/contact_mailer.rb
	class ContactMailer < ApplicationMailer
		def say_hello(user){
			@user = user
	      	mail to:@user.email, subject:"Rails send mail test"
		}
	end

## 信件內容
app/views/contact_mailer 新增 say_hello.html.erb

## 新增user頁面
	rails generate scaffold User name:string email:string tel:string

## SMTP設定 Rails.application.configure
	config.action_mailer.delivery_method = :smtp
	  config.action_mailer.default_url_options = { host: "http://localhost:3000" }
	  config.action_mailer.smtp_settings = {
	    address:              'smtp.gmail.com',
	    port:                 587,
	    domain:               'gmail.com',
	    user_name:            'username',
	    password:             'useremail',
	    authentication:       'plain',
	    enable_starttls_auto: true
	  }


