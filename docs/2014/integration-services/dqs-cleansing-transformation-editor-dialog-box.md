---
title: Cuadro de diálogo Editor de transformación limpieza de DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssdqs.designer.cleansing.f1
- SQL12.SSDQS.DESIGNER.DQCONNECTION.F1
ms.assetid: 07e79641-71ee-45d0-a9ba-ed6f9f68f333
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cbb5ca8c048b42313b4776b4a2e4b99e44eec406
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66059420"
---
# <a name="dqs-cleansing-transformation-editor-dialog-box"></a>Cuadro de diálogo Editor de transformación Limpieza de DQS
  Use el cuadro de diálogo **Editor de transformación Limpieza de DQS** para corregir datos con Data Quality Services (DQS). Para más información, consulte [Data Quality Services Concepts](../../2014/data-quality-services/data-quality-services-concepts.md).  
  
 Para obtener más información acerca de la transformación, vea [DQS Cleansing Transformation](data-flow/transformations/dqs-cleansing-transformation.md).  
  
 **¿Qué desea hacer?**  
  
-   [Abrir el Editor de transformación Limpieza de DQS](#open)  
  
-   [Establecer opciones en la pestaña Administrador de conexiones](#connection)  
  
-   [Establecer opciones en la pestaña Asignación](#mapping)  
  
-   [Establecer opciones en la pestaña Avanzadas](#advanced)  
  
-   [Establecer las opciones en el cuadro de diálogo Administrador de conexiones de limpieza de DQS](#manager)  
  
##  <a name="open"></a> Abrir el Editor de transformación Limpieza de DQS  
  
1.  Agregue la Transformación Limpieza de DQS al paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en el componente y, después, haga clic en **Editar**.  
  
##  <a name="connection"></a> Establecer opciones en la pestaña Administrador de conexiones  
 **Administrador de conexiones de calidad de datos**  
 Seleccione un administrador de conexiones DQS existente de la lista, o bien haga clic en **Nuevo**para crear una conexión.  
  
 **Nuevo**  
 Cree un administrador de conexiones con el cuadro de diálogo **Administrador de conexiones de limpieza de DQS** . Vea [Set the options in the DQS Cleansing Connection Manager dialog box](#manager).  
  
 **Base de conocimiento de calidad de datos**  
 Seleccione una base de conocimiento de DQS existente para el origen de datos conectado. Para obtener más información acerca de la base de conocimiento de DQS, vea [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Cifrar conexión**  
 Especifique si desea cifrar la conexión para cifrar la transferencia de datos entre el servidor DQS y [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 **Dominios disponibles**  
 Enumera los dominios disponibles para la base de conocimiento seleccionada. Hay dos tipos de dominios: dominios únicos y dominios compuestos que contienen dos o más dominios únicos.  
  
 Para obtener información acerca de cómo asignar columnas a dominios compuestos, vea [Map Columns to Composite Domains](data-flow/transformations/map-columns-to-composite-domains.md).  
  
 Para obtener más información acerca de los dominios, vea [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Configurar la salida de errores**  
 Especifica cómo se han de administrar los errores de fila. Pueden producirse errores cuando la transformación corrige los datos del origen de datos conectado, debido a restricciones de validación o valores de datos inesperados.  
  
 Los valores válidos son los siguientes:  
  
-   **Error de componente**, que indica que los errores de transformación y los datos de entrada no se insertan en la base de datos de Data Quality Services. Este es el valor predeterminado.  
  
-   **Redirigir fila**, que indica que los datos de entrada no se insertan en la base de datos de Data Quality Services y se redirigen a la salida de error.  
  
##  <a name="mapping"></a> Establecer opciones en la pestaña Asignación  
 Para obtener información acerca de cómo asignar columnas a dominios compuestos, vea [Map Columns to Composite Domains](data-flow/transformations/map-columns-to-composite-domains.md).  
  
 **Columnas de entrada disponibles**  
 Enumera las columnas del origen de datos conectado. Seleccione una o varias columnas que contengan los datos que desee corregir.  
  
 **Columna de entrada**  
 Muestra una columna de entrada que ha seleccionado en el área **Columnas de entrada disponibles** .  
  
 **Dominio**  
 Seleccione un dominio para asignar a la columna de entrada.  
  
 **Alias de origen**  
 Muestra la columna de origen que contiene el valor original de la columna.  
  
 Haga clic en este campo para modificar el nombre de columna.  
  
 **Alias de salida**  
 Muestra la columna devuelta por el **Editor de transformación Limpieza de DQS**. La columna contiene el valor original de la columna o el valor corregido.  
  
 Haga clic en este campo para modificar el nombre de columna.  
  
 **Alias de estado**  
 Muestra la columna que contiene información de estado sobre los datos corregidos. Haga clic en este campo para modificar el nombre de columna.  
  
##  <a name="advanced"></a> Establecer opciones en la pestaña Avanzadas  
 **Estandarizar salida**  
 Indica si los datos se van a generar en el formato estandarizado según el formato de salida que se haya definido para los dominios. Para más información sobre el formato estandarizado, vea [Limpieza de datos](../../2014/data-quality-services/data-cleansing.md).  
  
 **Confidence**  
 Indica si se debe incluir el nivel de confianza para los datos corregidos. El nivel de confianza indica el grado de certeza de DQS para la corrección o sugerencia. Para más información sobre los niveles de confianza, vea [Limpieza de datos](../../2014/data-quality-services/data-cleansing.md).  
  
 **Reason**  
 Indica si se debe incluir el motivo de la corrección de los datos.  
  
 **Datos anexados**  
 Indica si se van a generar datos adicionales que se hayan recibido de un proveedor de datos de referencia existente. Para obtener más información, consulte [Reference Data Services in DQS](../../2014/data-quality-services/reference-data-services-in-dqs.md).  
  
 **Esquema de datos anexados**  
 Indica si se va a generar el esquema de datos. Para obtener más información, vea [adjuntar un dominio o un dominio compuesto a datos de referencia](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md).  
  
##  <a name="manager"></a> Establecer las opciones en el cuadro de diálogo Administrador de conexiones de limpieza de DQS  
 **Nombre del servidor**  
 Seleccione o escriba el nombre del servidor DQS al que desee conectarse. Para obtener más información acerca del servidor, vea [DQS Administration](../../2014/data-quality-services/dqs-administration.md).  
  
 **Probar conexión**  
 Haga clic para confirmar que la conexión especificada es viable.  
  
 También puede abrir el cuadro de diálogo **Administrador de conexiones de limpieza de DQS** desde el área de conexiones; para ello, haga lo siguiente:  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] existente o cree uno nuevo.  
  
2.  Haga clic con el botón derecho en el área de conexiones, haga clic en **Nueva conexión**y, después, en **DQS**.  
  
3.  Haga clic en **Agregar**.  
  
## <a name="see-also"></a>Consulte también  
 [Aplicación de reglas de calidad de los datos al origen de datos](data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
  
