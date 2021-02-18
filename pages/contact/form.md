---
title: 'Contact Form'
form:
    name: contact
    fields:
        type:
            type: select
            size: long
            classes: 'fancy my-3'
            label: 'Support Category'
            help: 'Select the best category for your request'
            options:
                default: 'Select A Category'
                wallet: Wallet
                masternode: Masternode
                staking: Staking
        summary:
            label: Summary
            placeholder: 'Summarize your issue'
            type: text
            validate:
                required: true
        name:
            label: Name
            placeholder: 'Enter your first name or handle'
            autocomplete: 'on'
            type: text
            validate:
                required: true
        email:
            label: Email
            placeholder: 'Enter your email address'
            type: email
            validate:
                required: true
        message:
            label: Message
            size: long
            placeholder: 'Enter your message'
            type: textarea
            rows: 10
            style: 'width 600px'
            validate:
                required: true
        files:
            type: file
            multiple: true
            destination: 'user/data/{{ page.title }}'
            accept:
                - 'image/*'
                - file/txt
                - file/md
        note:
            type: honeypot
        g-recaptcha-response:
            label: Captcha
            type: captcha
            recaptcha_not_validated: 'Captcha not valid!'
    buttons:
        submit:
            type: submit
            value: Submit
        reset:
            type: reset
            value: Reset
    process:
        save:
            fileprefix: ticket-
            dateformat: Ymd-His-u
            extension: txt
            body: '{% include ''forms/data.txt.twig'' %}'
            operation: create
        discord: null
        message: 'Thank you for getting in touch!'
        display: thank-you
---

# New Ticket

Testing page.