---
title: Restaurar desde PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql11.asvs.ssmsimbi.RestoreFromPP.f1
ms.assetid: 232ac8ed-77fe-47d8-acd3-59bc2fdfdf48
author: minewiskan
ms.author: owend
ms.openlocfilehash: b153dfbe9dfdbb5741304153bd7b3dfd1d0d1b3c
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938676"
---
# <a name="restore-from-powerpivot"></a>Restaurar desde PowerPivot
  Puede utilizar la característica Restaurar desde PowerPivot en SQL Server Management Studio para crear una nueva base de datos de modelos tabulares en una instancia de Analysis Services (ejecutándose en modo tabular), o para llevar a cabo la restauración en una base de datos existente desde un libro PowerPivot (.xlsx).  
  
> [!NOTE]  
>  La plantilla de proyecto Importar desde PowerPivot de SQL Server Data Tools proporciona una funcionalidad similar. Para obtener más información, vea [Importar desde PowerPivot &#40;&#41;tabular de SSAS ](import-from-power-pivot-ssas-tabular.md).  
  
 Al utilizar la característica Restaurar desde PowerPivot, tenga en cuenta lo siguiente:  
  
-   Para utilizar la restauración desde PowerPivot, es necesario haber iniciado sesión como miembro del rol de administrador del servidor en la instancia de Analysis Services.  
  
-   La cuenta de servicio de la instancia de Analysis Services debe tener permisos de lectura en el archivo de libro desde el que va a restaurar.  
  
-   De forma predeterminada, cuando se restaura una base de datos desde PowerPivot, la propiedad Información de suplantación de origen de datos de la base de datos de modelos tabulares se establece en Predeterminado, que especifica la cuenta de servicio de la instancia de Analysis Services. Se recomienda cambiar las credenciales de suplantación a una cuenta de usuario de Windows en Propiedades de la base de datos. Para más información, vea [Suplantación &#40;SSAS tabular&#41;](impersonation-ssas-tabular.md).  
  
-   Los datos del modelo de datos de PowerPivot se copiarán en una base de datos de modelos tabulares nueva o en una ya existente en la instancia de Analysis Services. Si el libro PowerPivot contiene tablas vinculadas, estas se volverán a crear como una tabla sin un origen de datos, de forma similar a una tabla creada mediante Pegar en nueva tabla.  
  
### <a name="to-restore-from-powerpivot"></a>Para restaurar desde PowerPivot  
  
1.  En SSMS, en la instancia de Active Directory en la que se va a realizar la restauración, haga clic con el botón secundario en **Bases de datos**y, a continuación, en **Restaurar desde PowerPivot**.  
  
2.  En el cuadro de diálogo **Restaurar desde PowerPivot**, en **Origen de restauración**, en **Archivo de copia de seguridad**, haga clic en **Examinar** y seleccione un archivo.abf o.xslx desde el que va a realizar la restauración.  
  
3.  En **Restaurar destino**, en **Restaurar base de datos**, escriba un nombre para una base de datos nueva o para una base de datos existente. Si no especifica ningún nombre, se usa el nombre del libro.  
  
4.  En **Ubicación de almacenamiento**, haga clic en **Examinar** y seleccione una ubicación para almacenar la base de datos.  
  
5.  En **Opciones**, deje activada **Incluir información de seguridad** . Al restaurar desde un libro PowerPivot, este valor no se aplica.  
  
## <a name="see-also"></a>Consulte también  
 [Bases de datos de modelo tabular &#40;SSAS tabular&#41;](tabular-model-databases-ssas-tabular.md)   
 [Importar desde PowerPivot &#40;SSAS tabular&#41;](import-from-power-pivot-ssas-tabular.md)  
  
  
