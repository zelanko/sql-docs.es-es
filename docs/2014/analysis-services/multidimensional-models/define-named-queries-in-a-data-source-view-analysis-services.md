---
title: Definir consultas con nombre en una vista del origen de datos (Analysis Services) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- named queries [Analysis Services], creating
- modifying named queries
- data source views [Analysis Services], named queries
ms.assetid: f09ba8aa-950e-4c0d-961e-970de13200be
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 81155cc3036fb0e71a1d56515c7218e2f106664b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105705"
---
# <a name="define-named-queries-in-a-data-source-view-analysis-services"></a>Definir consultas con nombre en una vista del origen de datos (Analysis Services)
  Una consulta con nombre es una expresión SQL representada como una tabla. En una consulta con nombre, puede especificar una expresión SQL para seleccionar las filas y columnas que devuelven una o más tablas de uno o más orígenes de datos. Una consulta con nombre es similar a cualquier otra tabla de una vista del origen de datos (DSV), con filas y relaciones, con la excepción de que la consulta con nombre se basa en una expresión.  
  
 Una consulta con nombre permite ampliar el esquema relacional de las tablas existentes en una DSV sin modificar el origen de datos subyacente. Por ejemplo, se puede usar una serie de consultas con nombre para dividir una compleja tabla de dimensiones en tablas de menores dimensiones y más sencillas, a fin de usarlas en dimensiones de base de datos. Una consulta con nombre también se puede usar para combinar varias tablas de base de datos de uno o varios orígenes de datos y formar una sola tabla de vista del origen de datos.  
  
## <a name="creating-a-named-query"></a>Crear una consulta con nombre  
  
> [!NOTE]  
>  No se puede agregar un cálculo con nombre a una consulta con nombre, ni se puede basar una consulta con nombre en una tabla que contenga un cálculo con nombre.  
  
 Cuando se crea una consulta con nombre, se debe especificar un nombre, la consulta SQL que devuelve las columnas y los datos de la tabla y, opcionalmente, una descripción de la consulta con nombre. La expresión SQL puede hacer referencia a otras tablas de la vista del origen de datos. Después de definir una consulta con nombre, la consulta SQL de una consulta con nombre se envía al proveedor del origen de datos y se valida en conjunto. Si el proveedor no encuentra ningún error en la consulta SQL, la columna se agrega a la tabla.  
  
 Las tablas y columnas a las que se hace referencia en la consulta SQL no se deben calificar o deben calificarse solo por el nombre de tabla Por ejemplo, para hacer referencia a la columna SaleAmount de una tabla, son válidos los valores `SaleAmount` o `Sales.SaleAmount` , pero `dbo.Sales.SaleAmount` genera un error.  
  
 **Nota** Cuando defina una consulta con nombre que realiza consultas en un origen de datos [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0, se producirá un error en una consulta con nombre que contiene una subconsulta correlacionada y una cláusula GROUP BY. Para obtener más información, vea el artículo sobre el [error interno con una instrucción SELECT que contiene una subconsulta correlacionada y GROUP BY](http://support.microsoft.com/kb/274729) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base.  
  
## <a name="add-or-edit-a-named-query"></a>Agregar o editar una consulta con nombre  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto o conéctese a la base de datos que contiene la vista del origen de datos en que desea agregar una consulta con nombre.  
  
2.  En el Explorador de soluciones, expanda la carpeta **Vistas del origen de datos** y luego haga doble clic en la vista del origen de datos.  
  
3.  En el panel **Tablas** o **Diagrama** , haga clic con el botón derecho en un área abierta y, después, haga clic en **Nueva consulta con nombre**.  
  
4.  En el cuadro de diálogo **Crear consulta con nombre** , realice las siguientes operaciones:  
  
    1.  En el cuadro de texto **Nombre** , escriba el nombre de la consulta.  
  
    2.  Si lo desea, en el cuadro de texto **Descripción** , escriba una descripción de la consulta.  
  
    3.  En el cuadro de lista **Origen de datos** , seleccione el origen de datos en el que se ejecutará la consulta con nombre.  
  
    4.  Escriba la consulta en el panel inferior o use las herramientas gráficas de creación de consultas para crear una consulta.  
  
    > [!NOTE]  
    >  La interfaz de usuario (UI) de generación de consultas depende del origen de datos. En lugar de ver una UI gráfica, puede obtener una UI genérica, basada en texto. Puede realizar las mismas tareas con estas interfaces diferentes, pero debe hacerlo de diferente forma. Para más información, vea [Cuadro de diálogo Crear o Editar consulta con nombre &#40;Analysis Services - Datos multidimensionales&#41;](../create-or-edit-named-query-dialog-box-analysis-services-multidimensional-data.md).  
  
5.  Haga clic en **Aceptar**. En el encabezado de tabla aparecerá un icono que muestra dos tablas superpuestas para indicar que la tabla ha sido reemplazada por una consulta con nombre.  
  
## <a name="see-also"></a>Vea también  
 [Vistas del origen de datos en modelos multidimensionales](data-source-views-in-multidimensional-models.md)   
 [Definir cálculos con nombre en una vista del origen de datos &#40;Analysis Services&#41;](define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  