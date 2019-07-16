---
title: Identificar la SKU de base de datos SQL de Azure adecuada para la base de datos local (Data Migration Assistant) | Microsoft Docs
description: Aprenda a usar Data Migration Assistant para identificar a la derecha de la SKU de base de datos SQL de Azure para la base de datos local
ms.custom: ''
ms.date: 05/06/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: 7d87df240d4b83e53ef8f670609d2c896df7fe62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054670"
---
# <a name="identify-the-right-azure-sql-databasemanaged-instance-sku-for-your-on-premises-database"></a>Identificar a la derecha de la SKU de instancia de base de datos administrada de SQL Azure para la base de datos local

Migrar bases de datos a la nube pueden ser complicados, especialmente al intentar seleccionar el mejor destino de la base de datos de Azure y la SKU de la base de datos. Es nuestro objetivo con la base de datos Migration Assistant (DMA) ayudar a resolver estas cuestiones y facilitar la migración de base de datos experiencia proporcionando estas recomendaciones de SKU en una salida de uso sencillo.

En este artículo se centra en la característica de recomendaciones de SKU de Azure SQL Database de DMA. La base de datos de SQL Azure tiene varias opciones de implementación, incluidas:

- Base de datos única
- Grupos elásticos
- Instancia administrada

Las recomendaciones de SKU de característica le permite identificar tanto las mínimas recomendadas único de Azure SQL database o SKU en función de los contadores de rendimiento recopilados de los equipos que aloja las bases de datos de instancia administrada. La característica proporciona recomendaciones relacionadas con los precios de nivel, el nivel de proceso y tamaño máximo de datos, así como el costo estimado por mes. También ofrece la capacidad para la masiva aprovisionar solo bases de datos y las instancias administradas de Azure para todas las bases de datos recomendados.

> [!NOTE]
> Esta funcionalidad está disponible actualmente solo a través de la interfaz de línea de comandos (CLI).

Las siguientes son instrucciones que le ayudarán a determinar las recomendaciones de SKU de base de datos de SQL Azure y aprovisionar bases de datos único correspondientes o las instancias administradas en Azure con DMA.

## <a name="prerequisites"></a>Requisitos previos

- Descargue e instale la versión más reciente de [DMA](https://aka.ms/get-dma). Si ya tiene una versión anterior de la herramienta, ábralo y le pedirá que actualice DMA.
- Asegúrese de que el equipo tiene [PowerShell versión 5.1](https://www.microsoft.com/download/details.aspx?id=54616) o versiones posteriores, que es necesario para ejecutar todos los scripts. Para obtener información acerca de qué versión de PowerShell está instalada en el equipo de findoug, consulte el artículo [descargar e instalar Windows PowerShell 5.1](https://docs.microsoft.com/skypeforbusiness/set-up-your-computer-for-windows-powershell/download-and-install-windows-powershell-5-1).
- Asegúrese de que el equipo tiene instalado el módulo de Powershell de Azure. Para obtener más información, vea el artículo [instalar el módulo Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.8.0).
- Compruebe que el archivo de PowerShell **SkuRecommendationDataCollectionScript.ps1**, que es necesario para recopilar los contadores de rendimiento, se instala en la carpeta DMA.
- Asegúrese de que el equipo en el que deberá realizar este proceso tiene permisos de administrador en el equipo que hospeda las bases de datos.

## <a name="collect-performance-counters"></a>Recopilar contadores de rendimiento

Es el primer paso en el proceso recopilar contadores de rendimiento para las bases de datos. Puede recopilar los contadores de rendimiento mediante la ejecución de un comando de PowerShell en el equipo que hospeda las bases de datos. DMA le proporciona una copia de este archivo de PowerShell, pero también puede usar su propio método para capturar los contadores de rendimiento del equipo.

No es necesario realizar esta tarea para cada base de datos individualmente. Los contadores de rendimiento recopilados desde un equipo se pueden utilizar para recomendar la SKU para todas las bases de datos hospedadas en el equipo.

1. En la carpeta DMA, busque el archivo de PowerShell SkuRecommendationDataCollectionScript.ps1. Este archivo es necesario para recopilar los contadores de rendimiento.

    ![Archivo de PowerShell que se muestra en la carpeta DMA](../dma/media/dma-sku-recommend-data-collection-file.png)

2. Ejecute el script de PowerShell con los argumentos siguientes:
    - **ComputerName**: El nombre del equipo que hospeda las bases de datos.
    - **OutputFilePath**: La ruta de acceso de archivo de salida para guardar los contadores recopilados.
    - **CollectionTimeInSeconds**: La cantidad de tiempo durante el cual desea recopilar datos del contador de rendimiento. Capturar los contadores de rendimiento de al menos 40 minutos en obtener una recomendación significativa. La duración de la captura, más precisa la recomendación será. Asegúrese también de que las cargas de trabajo se ejecutan las bases de datos deseado habilitar las recomendaciones más precisas.
    - **DbConnectionString**: La cadena de conexión que apunte a la base de datos maestra alojado en el equipo desde el que está recopilando datos del contador de rendimiento.

    Aquí es una invocación de ejemplo:

    ```
    .\SkuRecommendationDataCollectionScript.ps1
     -ComputerName Foobar1
     -OutputFilePath D:\counters2.csv
     -CollectionTimeInSeconds 2400
     -DbConnectionString "Server=localhost;Initial Catalog=master;Integrated Security=SSPI;"
    ```

    Cuando se ejecuta el comando, el proceso dará como resultado un archivo que incluye los contadores de rendimiento en la ubicación especificada. Puede usar este archivo como entrada para la siguiente parte del proceso, que proporcionará recomendaciones de SKU para la base de datos única y las opciones de las instancias administradas.

## <a name="use-the-dma-cli-to-get-sku-recommendations"></a>Usar la CLI de DMA para obtener recomendaciones de SKU

Use el archivo de salida de los contadores de rendimiento que creó como entrada para este proceso.

Para la opción de base de datos única, DMA proporcionará recomendaciones para la base de datos Azure SQL Database único plan de tarifa, el nivel de proceso y el tamaño máximo de los datos para cada base de datos, en el equipo. Si tiene varias bases de datos en el equipo, también puede especificar las bases de datos para el que desea que las recomendaciones. DMA también le proporcionará el costo mensual estimado para cada base de datos.

Instancia administrada, las recomendaciones de admiten un escenario de migración mediante lift-and-shift. Como resultado, DMA le proporcionará recomendaciones para la instancia administrada de Azure SQL Database tarifa, el nivel de proceso y el tamaño máximo de los datos para el conjunto de bases de datos en el equipo. Nuevamente, si tiene varias bases de datos en el equipo, también puede especificar las bases de datos para el que desea que las recomendaciones. DMA también le proporcionará el costo mensual estimado para la instancia administrada.

Para usar la CLI de DMA para obtener recomendaciones de SKU, en el símbolo del sistema, ejecute dmacmd.exe con los argumentos siguientes:

- **/Action=SkuRecommendation**: Escriba este argumento para ejecutar las evaluaciones de SKU.
- **/SkuRecommendationInputDataFilePath**: La ruta de acceso al archivo de contadores recopilado en la sección anterior.
- **/SkuRecommendationTsvOutputResultsFilePath**: La ruta de acceso para escribir los resultados de salida en formato TSV.
- **/SkuRecommendationJsonOutputResultsFilePath**: La ruta de acceso para escribir los resultados de salida en formato JSON.
- **/SkuRecommendationHtmlResultsFilePath**: Ruta de acceso para escribir los resultados de salida en formato HTML.

Además, seleccione uno de los argumentos siguientes:

- Evitar la actualización de precios
  - **/SkuRecommendationPreventPriceRefresh**: Si se establece en True, evita que la actualización de precios que se producen y se da por supuesto los precios de forma predeterminada. Utilizar si está ejecutando en modo sin conexión. Si no usa este parámetro, debe especificar los parámetros siguientes para obtener los precios más recientes en función de una región especificada.
- Obtener los precios más recientes
  - **/SkuRecommendationCurrencyCode**: La moneda en que se va a mostrar los precios (p. ej. "USD").
  - **/ SkuRecommendationOfferName**: Nombre de la oferta (p. ej. "MS-AZR - 0003P"). Para obtener más información, consulte el [detalles de la oferta de Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) página.
    - **/SkuRecommendationRegionName**: El nombre de la región (por ejemplo, "WestUS").
    - **/SkuRecommendationSubscriptionId**: Identificador de la suscripción.
    - **/AzureAuthenticationTenantId**: El inquilino de autenticación.
    - **/AzureAuthenticationClientId**: El identificador de cliente de la aplicación AAD que se usa para la autenticación.
    - Una de las opciones de autenticación siguientes:
      - Interactiva
        - **AzureAuthenticationInteractiveAuthentication**: Establecido en true para una ventana emergente de autenticación.
      - Basada en certificados
        - **AzureAuthenticationCertificateStoreLocation**: Se establece en la ubicación del almacén de certificados (por ejemplo, "CurrentUser").
        - **AzureAuthenticationCertificateThumbprint**: Se establece en la huella digital del certificado.
      - En función del token
        - **AzureAuthenticationToken**: Establecer en el token de certificado.

> [!NOTE]
> Para obtener el ClientId y TenantId para la autenticación interactiva, deberá configurar una nueva aplicación de AAD. Para obtener más información sobre la autenticación y obtener estas credenciales, en el artículo [ejemplos de código de API de facturación de Microsoft Azure: API de RateCard](https://azure.microsoft.com/resources/samples/billing-python-ratecard-api/), siga las instrucciones de **paso 1: Configurar una aplicación cliente nativa en su inquilino AAD**.

Por último, hay un argumento opcional que puede usar para especificar las bases de datos que se desean recomendaciones: 

- **/SkuRecommendationDatabasesToRecommend**: Una lista de bases de datos que se va a realizar recomendaciones. La base de datos nombres distinguen mayúsculas de minúsculas y deben (1) se encuentra en la entrada .csv, (2) cada uno se rodeado por comillas dobles y (3) se separados por un espacio entre los nombres (por ejemplo, /SkuRecommendationDatabasesToRecommend = "Database1" "Database2" "Database3") . Si se omite este parámetro asegurarse de que se proporcionan recomendaciones para todas las bases de datos de usuario identificados en el archivo .csv de entrada.  

A continuación se muestran algunos invocaciones de ejemplo:

**Ejemplo 1: Obtención de recomendaciones con los precios de forma predeterminada. Se utiliza cuando se ejecuta en modo sin conexión o cuando no tiene credenciales de autenticación.**

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true
```

**Ejemplo 2: Obtención de recomendaciones con los precios más recientes de la región especificada (por ejemplo, "UKWest").**

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationInteractiveAuthentication=true
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
```

**Ejemplo 3: Obtención de recomendaciones para las bases de datos específicas (p. ej. "TPCDS1G, EDW_3G, TPCDS10G").**

```
.\DmaCmd.exe /Action=SkuRecommendation 
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv" 
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv" 
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json" 
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html" 
/SkuRecommendationCurrencyCode=USD 
/SkuRecommendationOfferName=MS-AZR-0044p 
/SkuRecommendationRegionName=UKWest 
/SkuRecommendationSubscriptionId=<Your Subscription Id> 
/SkuRecommendationDatabasesToRecommend=“TPCDS1G” “EDW_3G” “TPCDS10G” 
/AzureAuthenticationInteractiveAuthentication=true 
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId> 
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
```

Para obtener recomendaciones de la base de datos única, el archivo de salida TSV tendrá el aspecto siguiente:

![Archivo de base de datos de solo PowerShell que se muestra en la carpeta DMA](../dma/media/dma-sku-recommend-single-db-recommendations.png)

Para obtener recomendaciones de la instancia administrada, el archivo de salida TSV tendrá el aspecto siguiente:

![Archivo de instancia administrada de PowerShell que se muestra en la carpeta DMA](../dma/media/dma-sku-recommend-mi-recommendations.png)

Sigue una descripción de cada columna en el archivo de salida.

- **DatabaseName** -el nombre de la base de datos.
- **MetricType** -Azure SQL Database recomienda única base de datos administrados/nivel de instancia.
- **MetricValue** -Azure SQL Database recomienda única base de datos administrados/SKU de instancia.
- **PricePerMonth** : el precio estimado mensual para la SKU correspondiente.
- **RegionName** : el nombre de la región de la SKU correspondiente. 
- **IsTierRecommended** -realizamos una recomendación de SKU mínima para cada nivel. A continuación, aplicamos la heurística para determinar el nivel correcto de la base de datos. Esto refleja qué nivel se recomienda para la base de datos. 
- **ExclusionReasons** : este valor está en blanco si se recomienda un nivel. Para cada nivel que no se recomienda, proporcionamos los motivos por qué lo no se ha seleccionado.
- **AppliedRules** -una notación breve de las reglas que se aplicaron.

El nivel recomendado final (es decir, **MetricType**) y el valor (es decir, **MetricValue**)-se encuentra donde el **IsTierRecommended** columna es TRUE - refleja la SKU mínima se requiere para que las consultas ejecutar en Azure con una tasa de éxito similar a las bases de datos de forma local. Instancia administrada, DMA actualmente admite las recomendaciones para la 8vcore más usados a 40vcore SKU. Por ejemplo, si la SKU mínima recomendada es S4 del nivel estándar, a continuación, elegir S3 o por debajo se generan consultas en tiempo de espera o no se pueden ejecutar.

El archivo HTML contiene esta información en un formato gráfico. Proporciona un medio fácil de usar para ver la recomendación final y la siguiente parte del proceso de aprovisionamiento. Obtener más información sobre la salida HTML está en la sección siguiente.

## <a name="provision-recommended-skus-to-azure"></a>Recomienda aprovisionar las SKU de Azure

Con tan solo unos clics, puede usar las recomendaciones que identifica al destino de aprovisionar las SKU de Azure a la que puede migrar las bases de datos. Puede usar el archivo HTML para la entrada de suscripción de Azure. elegir el plan de tarifa, proceso nivel y el tamaño máximo de datos para las bases de datos; y generar un script para aprovisionar las bases de datos. Puede ejecutar esta secuencia de comandos mediante PowerShell.

Puede realizar este proceso en un único equipo, o puede realizar en varios equipos para determinar las recomendaciones de SKU a escala. DMA actualmente resulta una experiencia sencilla y escalable permitiendo todo el proceso a través de la interfaz de línea de comandos.

Para información de aprovisionamiento de entrada y realizar cambios en las recomendaciones, actualice el archivo HTML de la manera siguiente.

**Para obtener recomendaciones de la base de datos única**

![Pantalla de recomendaciones de SKU de base de datos de SQL Azure](../dma/media/dma-sku-recommend-single-db-recommendations1.png)

1. Abra el archivo HTML y escriba la siguiente información:
    - **Id. de suscripción** -el identificador de suscripción de la suscripción de Azure a la que desea aprovisionar las bases de datos.
    - **Grupo de recursos** : el grupo de recursos al que desea implementar las bases de datos. Escriba un grupo de recursos existente.
    - **Región** -la región en que se va a aprovisionar las bases de datos. Asegúrese de que la suscripción es compatible con la región que seleccione.
    - **Nombre del servidor** -servidor de la base de datos SQL de Azure al que desea que las bases de datos implementadas. Si escribe un nombre de servidor que no existe, se creará.
    - **Admin Username** -el nombre de usuario de administrador del servidor.
    - **Contraseña de administrador** -la contraseña de administrador del servidor. La contraseña debe tener al menos ocho caracteres y no más de 128 caracteres de longitud. La contraseña debe contener caracteres de tres de las siguientes categorías: inglés mayúsculas, letras minúsculas, números (0-9) y caracteres no alfanuméricos (!, $, #, %, etcetera.). La contraseña no puede contener todo o parte (3 + letras seguidas) desde el nombre de usuario.

2. Revise las recomendaciones para cada base de datos y modificar el plan de tarifa, proceso nivel y el tamaño de datos máximo según sea necesario. Asegúrese de anular la selección de las bases de datos que actualmente no desee aprovisionar.

3. Seleccione **generar Script de aprovisionamiento**, guarde el script y, a continuación, ejecutarlo en PowerShell.

    Este proceso debe crear todas las bases de datos que seleccionó en la página HTML.

**Para obtener recomendaciones de la instancia administrada**

![Pantalla de recomendaciones de SKU de MI SQL Azure](../dma/media/dma-sku-recommend-mi-recommendations1.png)

1. Abra el archivo HTML y escriba la siguiente información:
    - **Id. de suscripción** -el identificador de suscripción de la suscripción de Azure a la que desea aprovisionar las bases de datos.
    - **Grupo de recursos** : el grupo de recursos al que desea implementar las bases de datos. Escriba un grupo de recursos existente.
    - **Región** -la región en que se va a aprovisionar las bases de datos. Asegúrese de que la suscripción es compatible con la región que seleccione.
    - **Nombre de instancia** : la instancia de Azure SQL Managed Instance a la que van a migrar las bases de datos. El nombre de instancia puede contener solo letras minúsculas, números y '-', pero no puede comenzar ni terminar con '-' ni tener más de 63 caracteres.
    - **Instancia Admin Username** : el nombre de usuario del Administrador de instancia. Asegúrese de que el nombre de inicio de sesión cumple los requisitos siguientes: es un identificador de SQL y no un nombre de sistema típico (como admin, administrador, sa, root, dbmanager, loginmanager, etc.), o un usuario de base de datos integrada o rol (como dbo, guest, public, etcetera.). Asegúrese de que el nombre no contiene espacios en blanco, caracteres Unicode o caracteres no alfabéticos y que no comenzar con números o símbolos. 
    - **Contraseña de administrador de la instancia** -la contraseña de administrador de la instancia. La contraseña debe tener al menos 16 caracteres y no más de 128 caracteres de longitud. La contraseña debe contener caracteres de tres de las siguientes categorías: inglés mayúsculas, letras minúsculas, números (0-9) y caracteres no alfanuméricos (!, $, #, %, etcetera.). La contraseña no puede contener todo o parte (3 + letras seguidas) desde el nombre de usuario.
    - **Nombre de red virtual** : nombre de la red virtual en la que se debe aprovisionar la instancia administrada. Escriba un nombre de red virtual existente.
    - **Nombre de subred** : nombre de la subred en la que se debe aprovisionar la instancia administrada. Escriba un nombre de subred existente.

2. Revise las recomendaciones para cada instancia y modificar el plan de tarifa, proceso nivel y el tamaño de datos máximo según sea necesario. Mientras que las recomendaciones están limitadas actualmente a 8vcore a SKU 40vcore, sigue siendo la opción de aprovisionar SKU 64vcore y 80vcore si lo desea. Asegúrese de anular la selección de todas las instancias que no actualmente desee aprovisionar.

    Este proceso debe crear todas las bases de datos que seleccionó en la página HTML.

    > [!NOTE]
    > Creación de instancias administradas en una subred (especialmente para la primera vez), puede tardar varias horas en completarse. Después de ejecutar el script de aprovisionamiento a través de PowerShell, puede comprobar el estado de la implementación en Azure Portal.

## <a name="next-step"></a>Paso siguiente

- Para obtener una lista completa de comandos para ejecutar DMA desde la CLI, consulte el artículo [ejecutar Data Migration Assistant desde la línea de comandos](https://docs.microsoft.com/sql/dma/dma-commandline?view=sql-server-2017).
