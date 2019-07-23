---
title: Trabajar con suscripciones (portal web) | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 09e8ece5-0200-41f2-87c1-9fab19e261be
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 786f7391d87799a0822f357e449db21fea0d0f09
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68221251"
---
# <a name="working-with-subscriptions-web-portal"></a>Trabajar con suscripciones (portal web)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Use la página Suscripciones para mostrar todas las suscripciones del informe actual. Si tiene permisos suficientes, concedidos por la tarea "Administrar todas las suscripciones", puede ver las suscripciones de todos los usuarios. En caso contrario, esta página solo muestra las suscripciones que le pertenecen.  
  
Para poder crear una suscripción nueva, debe comprobar primero si el origen de datos de informe usa credenciales almacenadas. Use la página de propiedades Orígenes de datos para almacenar las credenciales.  
  
> [!NOTE]
> El servicio del Agente SQL Server debe estar iniciado.   
  
![ssRSWebPortal-subscriptions1](../reporting-services/media/ssrswebportal-subscriptions1.png)  
   
Para llegar a la página Suscripciones, haga clic en el botón de **puntos suspensivos (...)** de un informe, seleccione **Administrar** y seleccione **Suscripciones**.  
  
Para crear suscripciones en la página Suscripciones, seleccione **+ Nueva suscripción**. También puede editar las suscripciones existentes o eliminar las suscripciones que haya seleccionado.  
  
Esta página también proporciona el estado de los resultados de las ejecuciones de suscripción en la columna **Resultado** . Si se ha producido un error en una suscripción, nos interesa consultar la columna de resultados antes de nada para saber cuál fue el mensaje.  
  
## <a name="creating-or-editing-a-subscription"></a>Crear o editar una suscripción  
Use la página Nueva suscripción o Editar suscripción para crear una nueva suscripción a un informe o modificar una existente. Las opciones de esta página varían dependiendo de los roles que tenga asignados. Los usuarios con permisos avanzados pueden trabajar con más opciones.  
  
Las suscripciones se admiten para informes que se pueden ejecutar en modo desatendido. Como mínimo, el informe debe usar credenciales almacenadas o ninguna credencial. Si el informe utiliza parámetros, debe especificarse un valor predeterminado. Las suscripciones pueden pasar a estar inactivas si se cambia la configuración de ejecución del informe o si se quitan los valores predeterminados que se utilizan en las propiedades de los parámetros. Para más información, vea [Crear y administrar suscripciones para servidores de informes en modo nativo].  
  
### <a name="type-of-subscription"></a>Tipo de suscripción  
Puede optar entre una **suscripción estándar** y una **suscripción controlada por datos**.  
  
![ssRSWebPortal-subscriptions3](../reporting-services/media/ssrswebportal-subscriptions3.png)  
   
Una suscripción controlada por datos es aquella que consulta una base de datos de suscriptor para obtener información sobre la suscripción cada vez que esta se ejecuta. Las suscripciones controladas por datos usan los resultados de la consulta para determinar los destinatarios de la suscripción, la configuración de entrega y los valores de parámetro de informe. En tiempo de ejecución, el servidor de informes ejecuta una consulta para obtener los valores utilizados para la configuración de la suscripción.   
  
Para crear una suscripción controlada por datos, es necesario saber cómo escribir una consulta o un comando que obtenga los datos de la suscripción. También debe tener un almacén de datos que contenga los datos de suscriptor (por ejemplo, nombres de suscriptor y direcciones de correo electrónico) para usarlos para la suscripción.  
  
Esta opción está disponible para los usuarios con permisos avanzados. Si se usa la seguridad predeterminada, no se pueden utilizar suscripciones controladas por datos en los informes situados en la carpeta Mis informes.  
  
### <a name="destination"></a>Destino  
Seleccione la extensión de entrega que se va a utilizar para distribuir el informe.   
  
La disponibilidad de una extensión de entrega depende de si está instalada y configurada en el servidor de informes. El correo electrónico del Servidor de informes es la extensión de entrega predeterminada, pero debe configurarla primero para poder utilizarla. No es necesario configurar la entrega al recurso compartido de archivos, pero se debe definir una carpeta compartida para poder utilizarla.  
  
![ssRSWebPortal-subscriptions2](../reporting-services/media/ssrswebportal-subscriptions2.png)  
  
Según la extensión de entrega que usted seleccione, aparece la siguiente configuración:  
  
-   En las suscripciones por correo electrónico, se incluyen campos que son conocidos para los usuarios del correo electrónico, como Para, Asunto y Prioridad. Especifique **Incluir informe** para incrustar o adjuntar el informe, o **Incluir vínculo** , para incluir una dirección URL en el informe. Especifique **Formato de representación** para elegir un formato de presentación para el informe que ha adjuntado o incrustado.  
  
-   La suscripción a recursos compartidos de archivos proporciona campos que permiten especificar una ubicación de destino. Puede entregar cualquier informe a un recurso compartido de archivos. Sin embargo, los informes que admiten características interactivas, como los informes matriciales que permiten obtener detalles de filas y columnas complementarias, se representan como archivos estáticos. En este tipo de archivos, no es posible ver filas y columnas de detalle. El nombre del recurso compartido de archivos debe especificarse con el formato UNC (Convención de nomenclatura universal); por ejemplo: \miEquipo\public\misArchivosDeInformes. No incluya una barra inversa al final del nombre de la ruta de acceso. El archivo del informe se entregará en un formato de archivo basado en el formato de representación (por ejemplo, si elige Excel, el informe se entrega como archivo .xlsx).  
  
### <a name="data-driven-subscription-dataset"></a>Conjunto de datos de suscripción controlada por datos  
En una suscripción controlada por datos hay que definir el conjunto de datos que se usará para la suscripción. Seleccione **Editar conjunto de datos** para proporcionar esa información.  
  
![ssRSWebPortal-subscriptions4](../reporting-services/media/ssrswebportal-subscriptions4.png)  
  
Primero hay que suministrar un **origen de datos** para usarlo en la consulta. Puede tratarse de un origen de datos compartido, o bien puede proporcionar un origen de datos personalizado.  
  
Deberá proporcionar una **consulta** que enumere las distintas opciones necesarias para que la suscripción se ejecute. La pantalla proporcionará los campos que deben devolverse. Estos campos variarán según el método de entrega y los parámetros del informe.  
  
Para obtener los mejores resultados, ejecute primero la consulta en SQL Server Management Studio, antes de usarla en la suscripción controlada por datos. A continuación, puede examinar los resultados para comprobar que contiene la información requerida. Los puntos importantes para reconocer los resultados de la consulta son:  
  
-   Las columnas del conjunto de resultados determinan los valores que se pueden especificar para las opciones de entrega y los parámetros de informe. Por ejemplo, si está creando una suscripción controlada por datos para la entrega de correo electrónico, debería tener una columna de direcciones de correo electrónico.  
  
-   Las filas del conjunto de resultados determinan el número de entregas de informes que se generan. Si tiene 10.000 filas, el servidor de informes generará 10.000 notificaciones y entregas.  
  
![ssRSWebPortal-subscriptions5](../reporting-services/media/ssrswebportal-subscriptions5.png)  
  
Ya podemos pasar a validar la consulta. También se puede definir un **tiempo de espera de consulta**.  
  
Una vez creada la consulta, puede asignar valores a los campos obligatorios. Puede hacerlo escribiendo los datos manualmente o seleccionando un campo del conjunto de datos que ha creado.

[Portal web](../reporting-services/web-portal-ssrs-native-mode.md)  
[Trabajo con informes paginados](working-with-paginated-reports-web-portal.md)  
[Trabajo con conjuntos de datos compartidos](../reporting-services/work-with-shared-datasets-web-portal.md)

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
