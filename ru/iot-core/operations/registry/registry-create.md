# Создание реестра

{% list tabs %}

- CLI
  
  {% include [cli-install](../../../_includes/cli-install.md) %}
  
  {% include [default-catalogue](../../../_includes/default-catalogue.md) %}
  
  1. Создайте реестр:
  
     ```
     $ yc iot registry create --name my-registry
  
      id: b91ki3851hab9m0l68je
      folder_id: aoek49ghmknnpj1ll45e
      created_at: "2019-05-28T11:29:42.420Z"
      name: my-registry
     ```
  
     {% include [name-format](../../../_includes/name-format.md) %}
  
  1. Проверьте, что реестр создался:
  
      ```
      $ yc iot registry list
       +----------------------+-------------+
       |          ID          |    NAME     |
       +----------------------+-------------+
       | b91ki3851hab9m0l68je | my-registry |
       +----------------------+-------------+
      ```

- Terraform 

   {% include [terraform-definition](../../../solutions/_solutions_includes/terraform-definition.md) %}

   Если у вас ещё нет Terraform, [установите его и настройте провайдер Яндекс.Облака](../../../solutions/infrastructure-management/terraform-quickstart.md#install-terraform).  
   
   {% note info %}

   Чтобы добавить сертификаты реестру, [подготовьте](../certificates/create-certificates.md) их заранее.

   {% endnote %}

   Чтобы создать реестр устройств: 
     
   1. Опишите в конфигурационном файле параметры ресурса, который необходимо создать:
      
      * `yandex_iot_core_registry` — параметры реестра:
        * `name` — имя реестра.
        * `description` — описание реестра.
        * `labels` — метки реестра в формате `ключ:значение`.
        * `passwords` — список паролей реестра для авторизации с помощью [логина и пароля](../../concepts/authorization.md#log-pass).
        * `certificates` — список сертификатов реестра для авторизации с помощью [сертификатов](../../concepts/authorization.md#certs).
             
      Пример структуры ресурса в конфигурационном файле:
      
      ```
      resource "yandex_iot_core_registry" "my_registry" {
        name        = "test-registry"
        description = "test registry for terraform provider documentation"
        labels = {
          test-label = "label-test"
        }

        passwords = [
          "<пароль 1>",
          "<пароль 2>"
        ]

        certificates = [
          file("<путь к первому файлу с сертификатом>"),
          file("<путь ко второму файлу с сертификатом>")
        ]
      }

      output "yandex_iot_core_registry_my_registry" {
        value = "${yandex_iot_core_registry.my_registry.id}"
      }
      ```
      
      Более подробную информацию о ресурсах, которые вы можете создать с помощью Terraform, см. в [документации провайдера](https://www.terraform.io/docs/providers/yandex/index.html).
      
   2. Проверьте корректность конфигурационных файлов.
      
      1. В командной строке перейдите в папку, где вы создали конфигурационный файл.
      2. Выполните проверку с помощью команды:
         ```
         $ terraform plan
         ```
      Если конфигурация описана верно, в терминале отобразится список создаваемых ресурсов и их параметров. Если в конфигурации есть ошибки, Terraform на них укажет. 
         
   3. Разверните облачные ресурсы.

      1. Если в конфигурации нет ошибок, выполните команду:
         ```
         $ terraform apply
         ```
      2. Подтвердите создание ресурсов.
      
      После этого в указанном каталоге будут созданы все требуемые ресурсы. Проверить появление ресурсов и их настройки можно в [консоли управления]({{ link-console-main }}).

{% endlist %}
