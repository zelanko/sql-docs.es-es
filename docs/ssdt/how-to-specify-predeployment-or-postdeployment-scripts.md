---
title: Especificación de scripts anteriores o posteriores a la implementación | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7f78f517-f13d-4f4b-84b9-e804cb490b2c
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c328942196d4dfe5eea33c8e21e234c3fa453fa6
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094677"
---
# <a name="how-to-specify-predeployment-or-postdeployment-scripts"></a>Cómo: Especificar scripts anteriores o posteriores a la implementación
Los scripts anteriores y posteriores a la implementación ejecutan instrucciones de Transact\-SQL antes y después del script de implementación principal, que se genera a partir del proyecto de base de datos. Un proyecto solo puede tener un script anterior a la implementación y un script posterior a la implementación. Estos scritps se pueden usar para muchos propósitos. Por ejemplo:  
  
-   Un script anterior a la implementación puede copiar datos de una tabla que se vaya a convertir en una tabla temporal antes de volver a dar formato a los datos y aplicarlos a la tabla modificada en un script posterior a la implementación.  
  
-   Puede insertar datos de referencia que deban figurar en una tabla en un script posterior a la implementación. Antes de insertar los datos, puede probar si la tabla ya contiene datos. Si la tabla no está vacía, debe borrar los datos existentes o especificar que desea volver a crear siempre la base de datos antes de implementarla. Puede agregar una instrucción como la siguiente en el script posterior a la implementación:  
  
```  
IF (EXISTS(SELECT * FROM [dbo].[MyReferenceTable]))  
BEGIN  
    DELETE FROM [dbo].[MyReferenceTable]  
END  
```  
  
## <a name="to-add-and-modify-a-pre--or-post-deployment-script"></a>Para agregar un script anterior o posterior a la implementación  
  
1.  En el **Explorador de soluciones**, expanda el proyecto de base de datos para mostrar la carpeta Scripts.  
  
2.  Haga clic con el botón secundario del mouse en la carpeta Scripts y seleccione Agregar.  
  
3.  Seleccione Scripts en el menú contextual.  
  
4.  Seleccione un script anterior o posterior a la implementación. Si lo desea, especifique un nombre distinto del predeterminado. Haga clic en Agregar para finalizar.  
  
5.  Haga doble clic en el archivo en la carpeta Scripts.  
  
    Se abre el editor de Transact\-SQL en el que se muestra el contenido del archivo.  
  
Puede usar sintaxis SQLCMD y variables en sus scripts y establecer estas variables en las propiedades del proyecto de base de datos. Por ejemplo:  
  
-   Puede utilizar sintaxis SQLCMD para incluir el contenido de un archivo en un script anterior o posterior a la implementación. Los archivos se incluyen y se ejecutan en el orden en que se definen: `:r .\myfile.sql`  
  
-   Puede usar sintaxis SQLCMD para hacer referencia a una variable en el script posterior a la implementación. Puede establecer la variable SQLCMD en las propiedades del proyecto o en un perfil de publicación:  
  
    ```  
    :setvar TableName MyTable  
    SELECT * FROM [$(TableName)]  
    ```  
  
Para obtener más información acerca del uso de SQLCMD en scripts, vea [Configuración del proyecto de base de datos](../ssdt/database-project-settings.md).  
  
## <a name="see-also"></a>Ver también  
[Desarrollo de bases de datos sin conexión orientado a proyectos](../ssdt/project-oriented-offline-database-development.md)  
  
