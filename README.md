#!/bin/bash
while true; do
    echo "パスワードマネージャーへようこそ！"
    echo "次の選択肢から入力してください(Add Password/Get Password/Exit):"
    read choice

    case $choice in
        "Add Password")
            read -p "サービス名を入力してください: " serviceName
            read -p "ユーザー名を入力してください: " userName
            read -s -p "パスワードを入力してください: " password
            echo "$serviceName:$userName:$password" >> passwords.txt
            echo "パスワードの追加は成功しました。"
            ;;
        "Get Password")
            read -p "サービス名を入力してください: " serviceName
            password=$(grep "^$serviceName:" passwords.txt | cut -d: -f3)

            if [ -z "$password" ]; then
                echo "そのサービスは登録されていません。"
            else
                echo "サービス名：$serviceName"
                echo "ユーザー名：$(grep "^$serviceName:" passwords.txt | cut -d: -f2)"
                echo "パスワード：$password"
            fi
            ;;
        "Exit")
            echo "Thank you!"
            exit
            ;;
        *)
            echo "入力が間違えています。Add Password/Get Password/Exitから入力してください。"
            ;;
    esac
done
