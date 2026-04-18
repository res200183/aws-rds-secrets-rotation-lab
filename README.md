RDS MySQL + Secrets Manager Rotation
Небольшой проект, где я реализовал безопасное хранение и автоматическую ротацию пароля для RDS MySQL через AWS.
Что сделано
Поднят RDS MySQL (db.t3.micro)
Пароль генерируется и хранится в Secrets Manager
RDS использует секрет напрямую (без хардкода)
Настроена автоматическая ротация каждые 90 дней
Всё описано через CloudFormation (YAML)
Основная идея
Убрать хранение паролей в коде/файлах и передать это AWS:
Secrets Manager хранит и генерирует пароль
RotationSchedule + managed Lambda делают ротацию без ручной логики
Использованные ресурсы
AWS::RDS::DBInstance
AWS::SecretsManager::Secret
AWS::SecretsManager::SecretTargetAttachment
AWS::SecretsManager::RotationSchedule
Как развернуть
Через CLI: aws cloudformation create-stack --stack-name rds-rotation-lab --template-body file://template.yaml --capabilities CAPABILITY_NAMED_IAM
или через консоль CloudFormation (загрузить YAML)
Что можно улучшить
Multi-AZ
Backup retention > 0
Подключить приложение (EC2/ECS)
Добавить мониторинг
Зачем это нужно
Это типовой продакшн-паттерн: безопасное хранение секретов + автоматическая ротация без лишней операционки
