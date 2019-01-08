---
title: Origen XML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmlsource.f1
helpviewer_keywords:
- sources [Integration Services], XML
- XML source [Integration Services]
- XML Source Editor
ms.assetid: 68c27ea5-e93d-4e26-bfb2-d967ca0a5282
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7e8d49827c9f533c75933a316ff3b655d3f13025
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53353903"
---
# <a name="xml-source"></a>Origen XML
  El origen XML lee un archivo de datos XML y rellena las columnas de la salida de origen con los datos.  
  
 Los datos de los archivos XML suelen incluir relaciones jerárquicas. Por ejemplo, un archivo de datos XML puede representar catálogos y elementos en catálogos. Para que los datos puedan entrar en el flujo de datos, se debe determinar la relación de los elementos del archivo de datos XML y se debe generar una salida para cada elemento del archivo.  
  
## <a name="schemas"></a>Esquemas  
 El origen XML utiliza un esquema para interpretar los datos XML. Se puede usar un archivo de Definición de esquema XML (XSD) o esquemas insertados para traducir los datos XML a un formato tabular. Si configura el origen XML en el cuadro de diálogo **Editor de origen de XML** , la interfaz de usuario puede generar un XSD a partir del archivo de datos XML especificado.  
  
> [!NOTE]  
>  No se admiten DTD.  
  
 Los esquemas solo admiten un único espacio de nombres; no admiten colecciones de esquemas.  
  
> [!NOTE]  
>  El origen XML no valida los datos del archivo XML con el XSD.  
  
## <a name="xml-source-editor"></a>origen de XML, editor de  
 Los datos de los archivos XML suelen incluir relaciones jerárquicas. El cuadro de diálogo **Editor de origen de XML** utiliza el esquema especificado para generar las salidas del origen XML. Puede especificar un archivo XSD, usar un esquema insertado o generar un XSD del archivo de datos XML especificado. El esquema debe estar disponible en tiempo de diseño.  
  
 El origen XML genera estructuras tabulares a partir de los datos XML creando una salida para cada elemento que contenga otros elementos de los archivos XML. Por ejemplo, si los datos XML representan catálogos y elementos en catálogos, el origen XML crea una salida para catálogos y una salida para cada tipo de elemento de un catálogo. La salida de cada elemento contendrá columnas de salida para los atributos de ese elemento.  
  
 Para proporcionar información sobre la relación jerárquica de los datos en las salidas, el origen XML agrega a las salidas una columna que identifica el elemento primario para cada elemento secundario. Volviendo al ejemplo de los catálogos con distintos tipos de elementos, cada elemento tendría un valor de columna que identifica el catálogo al que pertenece.  
  
 El origen XML crea una salida para cada elemento, pero no es necesario utilizar todas las salidas. Puede eliminar cualquier salida que no desea utilizar o simplemente no conectarla a un componente de nivel inferior.  
  
 El origen XML también genera los nombres de las salidas para asegurarse de que no son ambiguos. Estos nombres pueden ser largos y es posible que no identifiquen las salidas de una manera útil. Puede cambiar los nombres de las salidas, con tal de que todos los nombres sean únicos. También puede modificar el tipo de datos y la longitud de las columnas de salida.  
  
 Para cada salida, el origen XML agrega una salida de error. De manera predeterminada, las columnas de salidas de error tienen el tipo de datos de cadena Unicode (DT_WSTR) con una longitud de 255, pero puede configurar las columnas en las salidas de error modificando su tipo de datos y su longitud.  
  
 Si el archivo de datos XML contiene elementos que no están en el XSD, estos elementos se omitirán y no se generará ninguna salida para ellos. Por otra parte, si en el archivo de datos XML falta algún elemento representado en el XSD, la salida contendrá columnas con valores NULL.  
  
 Cuando se extraen los datos del archivo de datos XML, se convierten a un tipo de datos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Pero el código del origen XML no puede convertir los datos XML en los tipos de datos DT_TIME2 o DT_DBTIMESTAMP2, ya que el origen no los admite. Para obtener más información, vea [Integration Services Data Types](integration-services-data-types.md).  
  
 Aunque el XSD o esquema insertado puede especificar el tipo de datos de los elementos, si no lo hace, el cuadro de diálogo **Editor de origen de XML** asignará el tipo de datos String Unicode (DT_WSTR) a la columna de la salida que contiene el elemento y establecerá la longitud de la columna en 255 caracteres.  
  
 Si el esquema especifica la longitud máxima de un elemento, la longitud de la columna de salida se establece en este valor. Si la longitud máxima es mayor que la longitud admitida por el tipo de datos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] al que se convierte el elemento, los datos se truncan en la longitud máxima del tipo de datos. Por ejemplo, si una cadena tiene una longitud de 5000, se trunca en 4000 caracteres porque la longitud máxima del tipo de datos DT_WSTR es 4000 caracteres; de igual modo, los datos BYTE se truncan en 8000 caracteres, la longitud máxima del tipo de datos DT_BYTES. Si el esquema no especifica la longitud máxima, la longitud predeterminada de las columnas con cualquiera de los tipos de datos se establece en 255. El truncamiento de datos en el origen de XML se controla de la misma manera que el truncamiento en otros componentes de flujo de datos. Para más información, vea [Control de errores en los datos](error-handling-in-data.md).  
  
 Puede modificar el tipo de datos y la longitud de columna. Para obtener más información, vea [Integration Services Data Types](integration-services-data-types.md).  
  
## <a name="configuration-of-the-xml-source"></a>Configuración del origen XML  
 El origen XML admite tres modos de acceso a datos distintos. Puede especificar la ubicación del archivo de datos XML, la variable que contiene la ubicación del archivo o la variable que contiene los datos XML.  
  
 El origen XML incluye las propiedades personalizadas `XMLData` y `XMLSchemaDefinition`, que se pueden actualizar a través de expresiones de propiedad al cargar el paquete. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas del origen XML](xml-source-custom-properties.md).  
  
 El origen XML admite varias salidas normales y varias salidas de error.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye el cuadro de diálogo **Editor de origen de XML**para configurar el origen XML. Este cuadro de diálogo está disponible en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de origen de XML** , haga clic en uno de los temas siguientes:  
  
-   [Editor de origen de XML &#40;página Administrador de conexiones&#41;](../xml-source-editor-connection-manager-page.md)  
  
-   [Editor de origen de XML &#40;página Columnas&#41;](../xml-source-editor-columns-page.md)  
  
-   [Editor de origen de XML &#40;página Salida de error&#41;](../xml-source-editor-error-output-page.md)  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](../common-properties.md)  
  
-   [Propiedades personalizadas del origen XML](xml-source-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Establecer las propiedades de un componente de flujo de datos](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Extraer datos mediante el origen de XML](xml-source.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Respuesta seleccionada, [Create an XML Destination for an SSIS Package](https://go.microsoft.com/fwlink/?LinkId=321993)(Crear un destino XML para un paquete SSIS), en curatedviews.cloudapp.net.  
  
  
