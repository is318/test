# test
@startuml
skinparam sequenceMessageAlign center
skinparam sequenceArrowThickness 2
skinparam roundcorner 10
skinparam ParticipantPadding 50
hide footbox

participant  Клиент #yellow 
participant ДБО
participant AWGW
participant БДПН
participant Провайдер

Group #grey Поиск вендора по номеру телефона
Клиент -> ДБО : Ввод номера телефона
ДБО     -> AWGW #yellow :MRPUPAY check=true по вендору MobilPhonePay
AWGW   -> БДПН :Запрос кода вендора
БДПН   -> AWGW :Возврат кода вендора
rnote over AWGW
Проверка по меню
"Вендоры БДПН New"
end note
AWGW   -> ДБО : "МТС"
ДБО     -> Клиент : "МТС"

end

Group Check
Клиент -> ДБО: Ввод суммы оплаты
activate ДБО #grey
ДБО     -> AWGW :MRPUPAY check=true по реальному вендору
activate AWGW #grey
AWGW   -> Провайдер :Проверка введенных данных
activate Провайдер #grey
Провайдер   -> AWGW :Данные проверены ОК
deactivate Провайдер
AWGW   -> ДБО : Данные проверены ОК
deactivate AWGW
deactivate ДБО
end

Group Pay
Клиент -> ДБО: Нажать "Оплатить"
activate ДБО #grey
ДБО     -> AWGW :MRPUPAY check=false по реальному вендору
activate AWGW #grey
AWGW   -> Провайдер :Проведение оплаты
activate Провайдер #grey
Провайдер   -> AWGW :Ответ по оплате
deactivate Провайдер
AWGW   -> ДБО : Ответ по оплате
deactivate AWGW
ДБО     -> Клиент : Ответ по оплате
deactivate ДБО
end

@enduml

