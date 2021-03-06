Static Content
==============

InfinniPlatform включает в себя хостинга статических файлов, таких как HTML, CSS, JavaScript, файлы изображений и прочие.

Преимущества:

#. Возможность отдавать статический контент клиенту по прямой ссылке.
#. Использование кэширования файлов браузером, и как следствие уменьшение нагрузки на сервер.


Static Content Configuration
----------------------------

В файле конфигурации AppExtension.json в секции ``staticContent`` необходимо задать соответствие физических путей (на диске) и виртуальных (в вебе) путей в ``StaticContentMapping``.
Пример конфигурации по умолчанию:

.. code-block:: json

  "staticContent": {
    "StaticContentMapping": {
      "/metadata": "content/metadata",
      "/": "content/www"
    }
  }

Таким образом файлы из папки ``<рабочая папка>\content\metadata`` будут доступны по пути ``http://<адрес приложения>/metadata``.
Пути до файлов и вложенных папок по умолчанию совпадать со структурой файлов и папок на диске.


.. important:: В целях безопасности, статические файлы могут находиться только внутри рабочей папки, т.о. пути вида "../content/metadata" - некорректны.

Static Content Configuration for UI
-----------------------------------

Механизм хостинга статических файлов можно использовать для хостинга UI, избавляясь таким образом от необходимости в веб-сервере (IIS, nginx).
Пример конфигурации:

.. code-block:: json

  "staticContent": {
    "StaticContentMapping": {
      /* www - папка, содержащая файлы UI */
      "/": "content/www"
    }
  }

.. warning:: Необходимо явно указывать точку входа, например http//<адрес приложения>/index.html (вместо http//<адрес приложения>/).


.. _resources-hosting:

Static Content Configuration for Resources
------------------------------------------

Для хоcтинга файлов, содержащихся в ресурсах сборки, в файле конфигурации AppExtension.json в секции ``staticContent`` небходимо задать соответствие физических путей (на диске) и виртуальных (в вебе) путей в ``ResourceContentMapping``.
Пример конфигурации:

.. code-block:: json

  "staticContent": {
    "ResourceContentMapping": {
      "/Resources/Sdk": "Sdk",
      "/ServiceHostResources": "ServiceHost"
    }
  }

Относительный путь до ресурса получается из пути до ресурса внутри сборки путем замены символов ``'.'`` на ``'/'``.
Имя сборки заменяется на путь указанный в файле конфигурации.

.. csv-table:: Пример преобразования путей до ресурсов сборки
   :header: "Путь внутри сборки", "Относительный путь"

    "Sdk.ResourceFile.txt", "/Resources/Sdk/ResourceFile.txt"
    "ServiceHost.ResourceFolder.ResourceFile.txt", "/ServiceHostResources/ResourceFolder/ResourceFile.txt"
