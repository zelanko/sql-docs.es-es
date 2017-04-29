---
title: "Acceso sin conexión a la documentación de SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 08/22/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 257ed357-8cbb-43bd-b042-254be5fbb977
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1266b0249a96fbc4828b2afee9fb218682501e4d
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-documentation-offline-access"></a>Acceso sin conexión a la documentación de SQL Server

Vea la documentación técnica sin conexión de SQL Server 2016.
  
## <a name="prerequisites"></a>Requisitos previos
Para ver la documentación técnica sin conexión de SQL Server 2016 necesita el Visor de Ayuda 2.2, que se instala con: 
- [Visual Studio 2015 (cualquier edición, incluida Community)](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) o
- [Vista previa de abril de 2016 de SQL Server Management Studio (SSMS) (13.0.12500.29) o posterior](https://msdn.microsoft.com/library/mt238290.aspx)

Instale cualquiera de estas ediciones antes de continuar con los pasos siguientes.
  
## <a name="install-sql-server-offline-technical-documentation"></a>Instalar la documentación técnica sin conexión de SQL Server 

1. Instale cualquier edición de Visual Studio 2015 o de la vista previa de abril de 2016 de SSMS o posterior. 
2. Inicie SSMS o Visual Studio.
3. En el menú **Ayuda** , situado en la barra de navegación superior, seleccione  **Agregar y quitar contenido de la Ayuda**. 

#### <a name="this-action-launches-the-helpviewer"></a>(Esta acción inicia el Visor de Ayuda).

4. En el Visor de Ayuda, elija el origen de instalación predeterminado: **En línea**. 
5. Haga clic en **Agregar** junto a toda la documentación que quiera instalar.
6. Haga clic en el botón **Actualización** , situado en la parte inferior derecha de la pantalla, para descargar e instalar la documentación seleccionada.
![Carga contenido sin conexión](../sql-server/media/load-offline-content.png) 

 >**IMPORTANTE** Cuando haga clic en actualizar, el Visor de Ayuda podría inmovilizarse o dejar de responder. A pesar de eso, ha descargado e instalado las opciones de documentación seleccionadas. **Para resolver este problema**, finalice el Visor de Ayuda en el Administrador de tareas y reinícielo siguiendo el paso 3 anterior. La primera vez que el Visor de Ayuda se inmovilice o deje de responder, siga también [estos pasos](https://msdn.microsoft.com/library/mt654096.aspx) . Solo necesita realizar estos pasos una vez, pero probablemente tenga que finalizar el Visor de Ayuda en el Administrador de tareas cada vez que actualice su contenido.  
6. Reinicie el Visor de Ayuda seleccionando otra vez Agregar y quitar contenido de la Ayuda. Ya puede usar la documentación sin conexión.



   ![Documentación sin conexión lista para su uso](../sql-server/media/offline-ready-to-use.png)




