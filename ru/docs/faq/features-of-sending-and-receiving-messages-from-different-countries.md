# Особенности отправки и получения сообщений на номера разных стран

* [Номера Мексики](#001)
* [Номера Аргентины](#002)
* [Номера Бразилии](#003)

## Номера Мексики {#001}

Во всех мексиканских номерах между кодом страны «52» и кодом города должна быть вставлена цифра «1» (так же для оператора Nextel). Код «11» в начале должен быть удалён. В итоге телефонный номер будет включать в себя 13 цифр: +52 1 XXX XXX XXXX.

> Исходный номер телефона +520123456789
> 
> Требуемый номер для отправки сообщений 5210123456789@c.us


## Номера Аргентины {#002}

Во всех аргентинских телефонных номерах между кодом страны «54» и кодом города должна быть вставлена цифра 9. Код «15» в начале должен быть удалён. В итоге телефонный номер будет включать в себя 13 цифр: +54 9 XXX XXX XXXX.

> Исходный номер телефона +540123456789
> 
> Требуемый номер для отправки сообщений 5490123456789@c.us
 

## Номера Бразилии {#003}

В некоторых регионах Бразилии в номер телефона добавлена цифра 9, между местным номером телефона и кодом региона Бразилии. Список кодов региона к которым необходимо добавлять цифру 9: 11-19, 21, 22, 24, 27, 28. Для номеров Бразилии с другими кодами региона, необходимо убирать цифру 9.

В итоге телефонный номер может включать в себя 12 или 13 цифр +55 21 (9) XXXX XXXX,
где 55 - код страны, 21 - код региона, ХХХХ ХХХХ - местный номер телефона.

> Исходный номер телефона +552112345678
> 
> Требуемый номер для отправки сообщений 5521912345678@c.us

??? success "Пример кода на python"
    
    Install the package
    ```
    pip install phonenumbers
    ```

    ```python
    import phonenumbers
    # is the only areas that whatspp updated for 9h digit
    UPDATED_AREA_CODE = {"55": ["11", "12", "13", "14", "15", "16", "17", "18", "19", "21", "22", "24", "27", "28"]}

    def prepare_whatsapp_number(phone):

        x = phonenumbers.parse(phone, None)
        country_code = str(x.country_code)
        area_code = str(x.national_number)[0:2]
        
        phone = phone.replace('+','')
        
        updated_area = UPDATED_AREA_CODE
        
        if updated_area.get(country_code):
            area_code_updated = updated_area[country_code]  

            # Remove or add the 9h digit for states that were not updated 
            if area_code not in area_code_updated:
                if len(str(x.national_number)) == 11:
                    phone = '%s%s%s' % (country_code, area_code, str(x.national_number)[3:])
            else:
                if len(str(x.national_number)) == 10:
                    phone = '%s%s%s%s' % (country_code, area_code,"9", str(x.national_number)[2:])
        
        return phone

    print(prepare_whatsapp_number("+559281386116"))
    print(prepare_whatsapp_number("+5592981386116")) #phone number not working
    ```

Информация взята из [статьи](https://support.gupshup.io/hc/ru/articles/4407840924953-A-brief-note-on-the-inconsistencies-for-mobile-numbers-and-their-WhatsApp-IDs-in-Brazil-digit-9-Mexico-digit-1-)
