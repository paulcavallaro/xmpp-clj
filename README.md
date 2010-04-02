# xmpp-clj

xmpp-clj allows you to write simple jabber bots in idiomatic clojure by providing a lightweight wrapper around the [smack](http://www.igniterealtime.org/projects/smack/) library.

## Usage
Create a temporary jabber account for your bot.  I've used gmail here, but there are a bunch of free providers
  
  
Create a leiningen project and cd into the project directory

    lein new mybot
    cd ./mybot
  
  
Add xmpp-clj to your deps (project.clj):


    (defproject testxmpp "1.0.0-SNAPSHOT"
      :description "FIXME: write"
      :dependencies [[org.clojure/clojure "1.1.0"]
                     [org.clojure/clojure-contrib "1.1.0"]
                     [xmpp-clj "0.1.0"]]
      :dev-dependencies [[leiningen/lein-swank "1.2.0-SNAPSHOT"]])
  
  
  
Open up src/mybot/core.clj and require the xmpp lib:

    (ns mybot.core
      (:require [xmpp-clj :as xmpp]))
<br />

Define your connection params:

    ;; Connection Info
    (def connect-info {:username "testclojurebot@gmail.com"
                       :password "clojurebot12345"
                       :host "talk.google.com"
                       :domain "gmail.com"})
		       
Add some logic, all this bot does is respond back to the sender with his/her message:
    
    ;; Important stuff
    (defn handle-message [message]
      (let [body (:body message)
            from-user (:from-name message)]
        (str "Hi " from-user ", you sent me " body)))


    ;; reload-helper allows you see changes to handle-message without restarting the bot.
    (defn reload-helper [message] 
        (handle-message message))

Define the bot

    (defonce x (xmpp/bot connect-info reload-helper))

    
Next, fire up your chat client, add your new buddy, and send him a message.  The response should look someting like this:

me: hello chatbot
chatbot: Hi zachary.kim@gmail.com, you sent me hello chatbot



See the src/smack_clj/examples directory for more useage examples.

## License

[Eclipse Public License v1.0](http://www.eclipse.org/legal/epl-v10.html)
