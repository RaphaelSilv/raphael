---
title: "Bash | Consuming API exchange"
date: 2020-03-02T14:33:42-04:00
description: ""
categories: ["Bash"]
dropCap: true
toc: false
displayInMenu: false
displayInList: true
draft: false
resources:
- name: featuredImage
  src: "mdd-coins.jpg"
  params:
    description: "A bunch of gold euro coins. A bunch of it."
---
<h5 style="color: gray" align="center"><a style="color: gray" href="https://pixabay.com/"><u>Pixabay</u><a/></h5>
<h2 style="color: black;"><i>"Happiness is only real when shared."</i></h2>
<h4 style="color: gray;">Christopher McCandless</h4>

## [Shell Currency Exchange](https://github.com/RaphaelSilv/shell-currency-exchange)

This shell script program aims to be a helpful tool in the daily basis of CLI users. This simple application provides real time currency information through API requisitions.

## Requirements

This project works with *http* [requisitions to an external API](https://www.currencyconverterapi.com/) for each time
you call the program. You must [generate your own key](https://free.currencyconverterapi.com/free-api-key) to be able to realize requisitions.

Inside `currency.sh` you can find the global variable `API_KEY`.

```sh
declare -r API_KEY="<MyKey>"
```

Paste the generated key into the quotes.

Also, make sure you have [curl](https://curl.haxx.se/) and [bc](https://curl.haxx.se/) properly installed. This application
works through those packages. You can easily try the following commands in your
shell to install the packages through =apt=:

```sh
 curl --version || apt-get install curl= and =bc --version >/dev/null || apt-get install
```


## How to Use it
Open a terminal or command prompt, paste the following command to it:
`
git clone https://github.com/RaphaelSilv/shell-currency.git
`

Inside =shell-currency= you can find =currency.sh= make sure to provide
execution rights through  [chmod](https://linux.die.net/man/1/chmod) command for it.

The last step is to add the absolute path to the file above to your environment
variables. If you use `zsh` or `bash` open your terminal, go to home and open =.bashrc or .zrsch=
with you favorite text editor and create an [alias](https://shapeshed.com/unix-alias/) as the following:

```bash
 alias <MyAlias>=<path>currency.sh
```

Close the terminal and open it again.

Now the try following command: `curr -f usd -t brl -a 1`

should produce an output similarly like so:

```sh
===================================
date: Sat, 25 Jan 2020 17:36:31 GMT

1 USD = 4.181404 BRL
===================================
```
#### Of course the value may change according to economical determinants.


## Help

The [API](https://free.currencyconverterapi.com/) used support the following currencies:

Each country has one 3 digits character used for requisitions. For instance:
`brl, usd, btc` correspond respectively to **American Dollar, Brazilian reais and
Bitcoin**

You can have more info in `curr -h`

## Clone us on github

[RaphaelSilv /shell-currency-exchange](https://github.com/RaphaelSilv/shell-currency-exchange)

## API'S sample codes

This project was added to the [API's sample codes](https://www.currencyconverterapi.com/docs) official documentation.
Over there you can find other usage examples that would fit better your needs or you can create an usage example that don't already exists and help the community.

## License

You can use this source code however you like. If necessary, please refer to the
API's [Terms of Service](https://www.currencyconverterapi.com/terms-of-service). If you appreciated the services provided, consider [buying the API maintainer a coffee](https://www.currencyconverterapi.com/buy-me-coffee)  as he is the one that has costs with domain, hosting, bandwidth
and, of course, with coffee.
