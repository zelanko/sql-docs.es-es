---
title: Importar desde una fuente de datos (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0686e519-67c2-4f9b-8cd2-84a4871499ee
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 27c22caf9c3b6dfebede60cd795496496562c19b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099845"
---
# <a name="import-from-a-data-feed-ssas-tabular"></a>Importar datos de una fuente de distribución de datos (SSAS tabular)
  Las fuentes de distribución de datos son uno o varios flujos de datos XML que se generan a partir de un origen de datos en línea y se transmiten a un documento o aplicación de destino. Puede importar datos desde una fuente de distribución de datos en el modelo mediante el Asistente para la importación de tablas.  
  
 Este tema contiene las siguientes secciones:  
  
-   [Descripción de la importación desde una fuente de distribución de datos](#prereq)  
  
-   [Importar datos de un conjunto de datos de Azure DataMarket](#azure)  
  
-   [Importar fuentes de distribución de datos de orígenes de datos públicos o corporativos](#importdata)  
  
-   [Importar fuentes de distribución de datos de listas de SharePoint](#importlist)  
  
-   [Importar fuentes de distribución de datos de informes de Reporting Services](#importreport)  
  
##  <a name="prereq"></a> Descripción de la importación desde una fuente de distribución de datos  
 En un modelo tabular, puede importar datos de los siguientes tipos de fuentes de distribución de datos:  
  
 **Informe de Reporting Services**  
 Puede usar un informe de Reporting Services publicado en un sitio de SharePoint o un servidor de informes como origen de datos en un modelo. Al importar datos de un informe de Reporting Services, se debe especificar un archivo de definición de informe (.rdl) como origen de datos.  
  
 **Conjunto de datos de Azure DataMarket**  
 Azure DataMarket es un servicio que proporciona un único canal de catálogo de soluciones y entrega de información como servicio basado en la nube. Los conjuntos de datos de Azure DataMarket requieren una clave de cuenta en lugar de una cuenta de usuario de Windows.  
  
 **Fuentes Atom**  
 La fuente debe ser una fuente Atom. No se admiten fuentes RSS. La fuente debe estar disponible públicamente o se debe tener permiso para conectarse a ella con una cuenta de Windows con la que se haya iniciado la sesión actual.  
  
 Los datos de una fuente de distribución de datos se agregan a un modelo una sola vez durante la importación. Para obtener datos actualizados desde la fuente, puede actualizar los datos desde el diseñador de modelos o configurar una programación de actualización de datos para el modelo una vez se haya implementado este en una instancia de producción de Analysis Services. Para más información, vea [Procesar datos &#40;SSAS tabular&#41;](process-data-ssas-tabular.md).  
  
##  <a name="azure"></a> Importar datos de un conjunto de datos de Azure DataMarket  
 Puede importar datos de un conjunto de datos de Azure DataMarket como una tabla en el modelo.  
  
#### <a name="to-import-data-from-an-azure-datamarket-dataset"></a>Para importar datos de un conjunto de datos de Azure DataMarket  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en el menú **Modelo** y, a continuación, haga clic en **Importar desde el origen de datos**. Se abre el Asistente para la importación de tablas.  
  
2.  En la página **Conectarse a un origen de datos** , en **Fuentes de distribución de datos**, seleccione **Conjunto de datos de Azure DataMarket**y, a continuación, haga clic en **Siguiente**.  
  
3.  En la página **Conectarse a un conjunto de datos de DataMarket Azure** , en **Nombre descriptivo**, escriba un nombre descriptivo para la fuente a la que está obteniendo acceso. Si está importando varias fuentes u orígenes de datos, el uso de nombres descriptivos para la conexión puede ayudarle a recordar cómo se usa la conexión.  
  
4.  En **Dirección URL de fuente de distribución de datos**, escriba la dirección para la fuente de distribución de datos.  
  
5.  En **Configuración de seguridad**, en **Clave de cuenta**, escriba una clave de cuenta. Analysis Services usa las claves de cuenta para tener acceso a las suscripciones de DataMarket.  
  
6.  Haga clic en **Probar conexión** para asegurarse de que la fuente está disponible. De forma alternativa, también puede hacer clic en **Avanzadas** para confirmar que la dirección URL base o la dirección URL del documento de servicio contiene la consulta o documento de servicio que proporciona la fuente.  
  
7.  Haga clic en **Siguiente** para continuar con la importación.  
  
8.  En la página **Información de suplantación** , especifique las credenciales que usará Analysis Services para conectarse con el origen de datos al actualizar los datos y, a continuación, haga clic en **Siguiente**. Estas credenciales son diferentes de la clave de cuenta.  
  
9. En la página del asistente **Seleccionar tablas y vistas** , en el campo **Nombre descriptivo** , escriba un nombre descriptivo que identifique la tabla que contendrá estos datos una vez se hayan importado.  
  
10. Haga clic en **Vista previa y filtro** para revisar los datos y cambiar las selecciones de columna. No puede restringir las filas que se importan de la fuente de distribución de datos del informe, pero puede quitar columnas. Haga clic en **Aceptar**.  
  
11. En la página **Seleccionar tablas y vistas** , haga clic en **Finalizar**.  
  
##  <a name="importdata"></a> Importar fuentes de distribución de datos de orígenes de datos públicos o corporativos  
 Puede tener acceso a fuentes públicas o servicios de datos personalizados que generen fuentes Atom desde sistemas de base de datos propios o heredados.  
  
#### <a name="to-import-data-from-public-or-corporate-data-feeds"></a>Para importar datos de fuentes de distribución de datos públicos o corporativos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en el menú **Modelo** y, a continuación, haga clic en **Importar desde el origen de datos**. Se abre el Asistente para la importación de tablas.  
  
2.  En la página **Conectarse a un origen de datos** , en **Fuentes de distribución de datos**, seleccione **Otras fuentes**y, a continuación, haga clic en **Siguiente**.  
  
3.  En la página **Conectarse a una fuente de distribución de datos** , escriba un nombre descriptivo para la fuente a la que está obteniendo acceso. Si está importando varias fuentes u orígenes de datos, el uso de nombres descriptivos para la conexión puede ayudarle a recordar cómo se usa la conexión.  
  
4.  En **Dirección URL de fuente de distribución de datos**, escriba la dirección para la fuente de distribución de datos. Los valores válidos incluyen los siguientes:  
  
    1.  Un documento XML que contiene los datos de Atom. Por ejemplo, la siguiente dirección URL señala a una fuente pública en el sitio web de Open Government Data Initiative:  
  
        ```  
        http://ogdi.cloudapp.net/v1/dc/banklocations/  
        ```  
  
    2.  Un documento .atomsvc que especifica una o más fuentes. Un documento .atomsvc señala a un servicio o aplicación que proporciona una o más fuentes. Cada fuente se especifica como una consulta básica que devuelve el conjunto de resultados.  
  
         Puede especificar una dirección URL para un documento .atomsvc que está en un servidor web o puede abrir el archivo desde una carpeta compartida o local en su equipo. Es posible que tenga un documento .atomsvc si guardó uno en el equipo mientras exportaba un informe de Reporting Services o bien, es posible que tenga documentos .atomsvc en una biblioteca de fuentes de distribución de datos que haya creado alguien para el sitio de SharePoint.  
  
        > [!NOTE]  
        >  Se recomienda especificar un documento .atomsvc al que se pueda tener acceso a través de una dirección URL o de una carpeta compartida porque ofrece la opción de configurar posteriormente la actualización automática de los datos para el libro, una vez haya publicado el libro en SharePoint. El servidor puede volver a utilizar la misma dirección URL o carpeta de red para actualizar los datos si especifica una ubicación que no sea local para el equipo.  
  
5.  Haga clic en **Probar conexión** para asegurarse de que la fuente está disponible. De forma alternativa, también puede hacer clic en **Avanzadas** para confirmar que la dirección URL base o la dirección URL del documento de servicio contiene la consulta o documento de servicio que proporciona la fuente.  
  
6.  Haga clic en **Siguiente** para continuar con la importación.  
  
7.  En la página **Información de suplantación** , especifique las credenciales que usará Analysis Services para conectarse con el origen de datos al actualizar los datos y, a continuación, haga clic en **Siguiente**.  
  
8.  En la página del asistente **Seleccionar tablas y vistas** , en el campo **Nombre descriptivo** , reemplace el contenido de la fuente de distribución de datos con un nombre descriptivo que identifique la tabla que contendrá estos datos una vez se hayan importado.  
  
9. Haga clic en **Vista previa y filtro** para revisar los datos y cambiar las selecciones de columna. No puede restringir las filas que se importan de la fuente de distribución de datos del informe, pero puede quitar columnas. Haga clic en **Aceptar**.  
  
10. En la página **Seleccionar tablas y vistas** , haga clic en **Finalizar**.  
  
##  <a name="importlist"></a> Importar fuentes de distribución de datos de listas de SharePoint  
 Puede importar cualquier lista de SharePoint que tenga un botón **Exportar como fuente de distribución de datos** en el menú de la cinta (SharePoint). Puede hacer clic en este botón para exportar la lista como una fuente.  
  
#### <a name="to-import-data-feeds-from-a-sharepoint-list"></a>Para importar fuentes de distribución de datos de una lista de SharePoint  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en el menú **Modelo** y, a continuación, haga clic en **Importar desde el origen de datos**.  
  
2.  En la página **Conectarse a un origen de datos** , en **Fuentes de distribución de datos**, seleccione **Otras fuentes**y, a continuación, haga clic en **Siguiente**.  
  
3.  En la página **Conectarse a una fuente de distribución de datos** , escriba un nombre descriptivo para la fuente a la que está obteniendo acceso. Si está importando varias fuentes u orígenes de datos, el uso de nombres descriptivos para la conexión puede ayudarle a recordar cómo se usa la conexión.  
  
4.  En la dirección URL de fuente de datos, escriba una dirección para el servicio de datos de lista, reemplazando \<server-name > por el nombre real del servidor de SharePoint:  
  
    ```  
    http://<server-name>/_vti_bin/listdata.svc  
    ```  
  
5.  Haga clic en **Probar conexión** para asegurarse de que la fuente está disponible. De forma alternativa, también puede hacer clic en **Avanzadas** para confirmar que la dirección URL del documento de servicio contiene una dirección para el servicio de datos de la lista.  
  
6.  Haga clic en **Siguiente** para continuar con la importación.  
  
7.  En la página **Información de suplantación** , especifique las credenciales que usará Analysis Services para conectarse con el origen de datos al actualizar los datos y, a continuación, haga clic en **Siguiente**.  
  
8.  En la página **Seleccionar tablas y vistas** del asistente, seleccione las listas que desea importar.  
  
    > [!NOTE]  
    >  Solo puede importar listas que contienen columnas.  
  
9. Haga clic en **Vista previa y filtro** para revisar los datos y cambiar las selecciones de columna. No puede restringir las filas que se importan de la fuente de distribución de datos del informe, pero puede quitar columnas. Haga clic en **Aceptar**.  
  
10. En la página **Seleccionar tablas y vistas** , haga clic en **Finalizar**.  
  
##  <a name="importreport"></a> Importar fuentes de distribución de datos de informes de Reporting Services  
 Si tiene una implementación de Reporting Services de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] , puede usar la extensión de representación de Atom para generar una fuente de distribución de datos a partir de un informe existente.  
  
#### <a name="to-import-report-data-from-a-published-reporting-services-report"></a>Para importar datos de informe de un informe de Reporting Services publicado  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en el menú **Modelo** y, a continuación, haga clic en **Importar desde el origen de datos**.  
  
2.  En la página **Conectarse a un origen de datos** , en **Fuentes de distribución de datos**, seleccione **Informe**y, a continuación, haga clic en **Siguiente**.  
  
3.  En la página Conectarse a un informe de Microsoft SQL Server Reporting Services, en el campo Nombre descriptivo de la conexión, escriba un nombre descriptivo para la fuente a la está obteniendo acceso. Si está importando varios orígenes de datos, el uso de nombres descriptivos para la conexión puede ayudarle a recordar cómo se usa la conexión.  
  
4.  Haga clic en **Examinar** y seleccione un servidor de informes.  
  
     Si usa regularmente los informes en un servidor de informes, el servidor puede aparecer en **Sitios y servidores recientes**. De lo contrario, en Nombre, escriba una dirección de un servidor de informes y haga clic en **Abrir** para examinar las carpetas en el sitio del servidor de informes. Un ejemplo de dirección para un servidor de informes puede ser http://\<nombreDeEquipo > / reportserver.  
  
5.  Seleccione el informe y, a continuación, haga clic en **Abrir**. Alternativamente, puede pegar un vínculo al informe, incluida la ruta de acceso completa y nombre del informe, en el cuadro de texto **Nombre** . El Asistente para la importación de tablas conecta con el informe y lo representa en el área de vista previa.  
  
     Si el informe utiliza parámetros, debe especificar un parámetro o no podrá crear la conexión al informe. Al hacer esto, solo las filas relacionadas con el valor del parámetro se importan en la fuente de distribución de datos.  
  
    1.  Elija un parámetro mediante el cuadro de lista o el cuadro combinado proporcionado en el informe.  
  
    2.  Haga clic en **Ver informe** para actualizar los datos.  
  
        > [!NOTE]  
        >  Al ver el informe, se guardan los parámetros que seleccionó junto con la definición de la fuente de distribución de datos.  
  
     De manera opcional, haga clic en **Avanzada** para establecer las propiedades específicas del proveedor para el informe.  
  
6.  Haga clic en **Probar conexión** para asegurarse de que el informe está disponible como fuente de distribución de datos. Alternativamente, también puede hacer clic en **Avanzada** para confirmar que la propiedad **Documento de servicio incorporado** contiene XML incrustado que especifica la conexión de fuente de distribución de datos.  
  
7.  Haga clic en **Siguiente** para continuar con la importación.  
  
8.  En la página **Información de suplantación** , especifique las credenciales que usará Analysis Services para conectarse con el origen de datos al actualizar los datos y, a continuación, haga clic en **Siguiente**.  
  
9. En la página **Seleccionar tablas y vistas** del asistente, active la casilla situada al lado de los elementos de informe que desea importar como datos.  
  
     Algunos informes pueden contener varios componentes, como tablas, listas o gráficos.  
  
10. En el cuadro **Nombre descriptivo** , escriba el nombre de la tabla donde desea que se guarde la fuente de distribución de datos en el modelo.  
  
     De forma predeterminada, se usa el nombre del control de Reporting Services si no se ha asignado ningún nombre: por ejemplo, Tablix1 o Tablix2. Recomendamos cambiar este nombre durante la importación para que pueda identificar el origen de la fuente de distribución de datos importada más fácilmente.  
  
11. Haga clic en **Vista previa y filtro** para revisar los datos y cambiar las selecciones de columna. No puede restringir las filas que se importan de la fuente de distribución de datos del informe, pero puede quitar columnas. Haga clic en **Aceptar**.  
  
12. En la página **Seleccionar tablas y vistas** , haga clic en **Finalizar**.  
  
## <a name="see-also"></a>Vea también  
 [Orígenes de datos admitidos &#40;Tabular de SSAS&#41;](tabular-models/data-sources-supported-ssas-tabular.md)   
 [Tipos de datos admitidos &#40;Tabular de SSAS&#41;](tabular-models/data-types-supported-ssas-tabular.md)   
 [Suplantación &#40;Tabular de SSAS&#41;](tabular-models/impersonation-ssas-tabular.md)   
 [Procesar datos &#40;Tabular de SSAS&#41;](process-data-ssas-tabular.md)   
 [Importar datos &#40;Tabular de SSAS&#41;](import-data-ssas-tabular.md)  
  
  
