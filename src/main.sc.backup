theme: /

    state: newNode_0
        script:
            $session.token = "токен" // токен бота
            $session.chatId = "-4107" // id чата группы в котором будет выполняться проверка
            $session.username = $session.rawRequest.message.from.username
            $session.clientId = $session.rawRequest.message.from.id // получаем user_id
        # Transition /newNode_1
        go!: /newNode_2

    state: newNode_2
        HttpRequest:
            url = https://api.telegram.org/bot${token}/getChatMember
            method = POST
            body = {
                "chat_id" : {{$session.chatId}},
                "user_id" : {{$session.clientId}}
                }
            okState = /newNode_3
            errorState = /newNode_4
            timeout = 0
            headers = []
            vars = [{"name":"Member","value":"$session.httpResponse.result.status"}]

    state: newNode_3
        if: $session.httpResponse.result.status == "member"
            go!: /newNode_5
        elseif: $session.httpResponse.result.status == "creator"
            go!: /newNode_5
        else:
            go!: /newNode_6

    state: newNode_4
        a: Ошибка {{$session.httpStatus}}

    state: newNode_5
        a: Вы подписчик

    state: newNode_6
        a: Вы не подписчик