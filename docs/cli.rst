
smokepy CLI
~~~~~~~~~~~
`smokepy` is a convenient CLI utility that enables you to manage your wallet, transfer funds, check
balances and more.

Using the Wallet
----------------
`smokepy` lets you leverage your BIP38 encrypted wallet to perform various actions on your accounts.

The first time you use `smokepy`, you will be prompted to enter a password. This password will be used to encrypt
the `smokepy` wallet, which contains your private keys.

You can change the password via `changewalletpassphrase` command.

::

    smokepy changewalletpassphrase


From this point on, every time an action requires your private keys, you will be prompted to enter
this password (from CLI as well as while using `smoke` library).

To bypass password entry, you can set an environmnet variable ``UNLOCK``.

::

    UNLOCK=mysecretpassword smokepy transfer 100 SMOKE <recipient>

Common Commands
---------------
First, you may like to import your Smoke account:

::

    smokepy importaccount


You can also import individual private keys:

::

   smokepy addkey <private_key>

Listing accounts:

::

   smokepy listaccounts

Show balances:

::

   smokepy balance account_name1 account_name2

Sending funds:

::

   smokepy transfer --account <account_name> 100 SMOKE <recipient_name> memo

Upvoting a post:

::

   smokepy upvote --account <account_name> https://smoke.io/smoke/@betgames/why-you-should-be-proud-of-being-a-part-of-smoke-io-family


Setting Defaults
----------------
For a more convenient use of ``smokepy`` as well as the ``smoke`` library, you can set some defaults.
This is especially useful if you have a single Smoke account.

::

   smokepy set default_account furion
   smokepy set default_vote_weight 100

   smokepy config
    +---------------------+--------+
    | Key                 | Value  |
    +---------------------+--------+
    | default_account     | furion |
    | default_vote_weight | 100    |
    +---------------------+--------+

If you've set up your `default_account`, you can now send funds by omitting this field:

::

    smokepy transfer 100 SMOKE <recipient_name> memo


Help
----
You can see all available commands with ``smokepy -h``

::

    ~ % smokepy -h
    usage: smokepy [-h] [--node NODE] [--no-broadcast] [--no-wallet] [--unsigned]
                   [--expires EXPIRES] [--verbose VERBOSE] [--version]
                   {set,config,info,changewalletpassphrase,addkey,delkey,getkey,listkeys,listaccounts,upvote,downvote,transfer,powerup,powerdown,powerdownroute,convert,balance,interest,permissions,allow,disallow,newaccount,importaccount,updatememokey,approvewitness,disapprovewitness,sign,broadcast,orderbook,buy,sell,cancel,resmoke,follow,unfollow,setprofile,delprofile,witnessupdate,witnesscreate}
                   ...

    Command line tool to interact with the Smoke network

    positional arguments:
      {set,config,info,changewalletpassphrase,addkey,delkey,getkey,listkeys,listaccounts,upvote,downvote,transfer,powerup,powerdown,powerdownroute,convert,balance,interest,permissions,allow,disallow,newaccount,importaccount,updatememokey,approvewitness,disapprovewitness,sign,broadcast,orderbook,buy,sell,cancel,resmoke,follow,unfollow,setprofile,delprofile,witnessupdate,witnesscreate}
                            sub-command help
        set                 Set configuration
        config              Show local configuration
        info                Show basic SMOKE blockchain info
        changewalletpassphrase
                            Change wallet password
        addkey              Add a new key to the wallet
        delkey              Delete keys from the wallet
        getkey              Dump the privatekey of a pubkey from the wallet
        listkeys            List available keys in your wallet
        listaccounts        List available accounts in your wallet
        upvote              Upvote a post
        downvote            Downvote a post
        transfer            Transfer SMOKE
        powerup             Power up (vest SMOKE as SMOKE POWER)
        powerdown           Power down (start withdrawing SMOKE from smoke POWER)
        powerdownroute      Setup a powerdown route
        balance             Show the balance of one more more accounts
        interest            Get information about interest payment
        permissions         Show permissions of an account
        allow               Allow an account/key to interact with your account
        disallow            Remove allowance an account/key to interact with your
                            account
        newaccount          Create a new account
        importaccount       Import an account using a passphrase
        updatememokey       Update an account's memo key
        approvewitness      Approve a witnesses
        disapprovewitness   Disapprove a witnesses
        sign                Sign a provided transaction with available and
                            required keys
        broadcast           broadcast a signed transaction
        orderbook           Obtain orderbook of the internal market
        buy                 Buy SMOKE from the internal market
        sell                Sell SMOKE from the internal market
        cancel              Cancel order in the internal market
        resmoke             Resmoke an existing post
        follow              Follow another account
        unfollow            unfollow another account
        setprofile          Set a variable in an account's profile
        delprofile          Set a variable in an account's profile
        witnessupdate       Change witness properties
        witnesscreate       Create a witness

    optional arguments:
      -h, --help            show this help message and exit
      --node NODE           URL for public Smoke API (default:
                            "https://api.smoke.io")
      --no-broadcast, -d    Do not broadcast anything
      --no-wallet, -p       Do not load the wallet
      --unsigned, -x        Do not try to sign the transaction
      --expires EXPIRES, -e EXPIRES
                            Expiration time in seconds (defaults to 30)
      --verbose VERBOSE, -v VERBOSE
                            Verbosity
      --version             show program's version number and exit

