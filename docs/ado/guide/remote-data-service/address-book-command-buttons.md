---
title: Botones de comando de libreta de direcciones | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address book application scenario [ADO], command buttons
- RDS scenarios [ADO], command buttons
ms.assetid: 80676831-6488-4dad-a558-c47c52256a22
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 531e10f28850e6da6f9863cb5f06e253793b1dee
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="address-book-command-buttons"></a>Botones de comando de libreta de direcciones
La aplicación de la libreta de direcciones incluye los siguientes botones de comando:  
  
-   A **buscar** botón para enviar una consulta a la base de datos.  
  
-   A **borrar** botón para borrar los cuadros de texto antes de iniciar una nueva búsqueda.  
  
-   Un **Actualizar perfil** botón para guardar los cambios en un registro del empleado.  
  
-   A **cancelar cambios** botón para descartar los cambios.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="find-button"></a>Botón Buscar  
 Al hacer clic en el **buscar** botón activa el procedimiento de subprocedimiento Find_OnClick de VBScript, que genera y envía la consulta SQL. Al hacer clic en este botón, se rellena la cuadrícula de datos.  
  
## <a name="building-the-sql-query"></a>Crear la consulta SQL  
 La primera parte del subprocedimiento Find_OnClick genera la consulta SQL, una frase a la vez, anexando cadenas de texto a una instrucción SQL SELECT global. Comienza estableciendo la variable `myQuery` a una instrucción SELECT de SQL que solicita todas las filas de datos de la tabla de origen de datos. A continuación, el subprocedimiento examina cada uno de los cuatro cuadros de entrada en la página.  
  
 Dado que el programa utiliza la palabra `like` en la creación de las instrucciones SQL, las consultas son búsquedas de subcadenas en lugar de coincidencias exactas.  
  
 Por ejemplo, si la **Last Name** cuadro contenía la entrada "Berge" y el **título** cuadro contenía la entrada "Program Manager", la instrucción SQL (valor de `myQuery`) leería:  
  
```  
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 Si la consulta se realizó correctamente, todas las personas con apellidos que contiene el texto "Berge" (tales como Berge y Berger) y con un título que contienen las palabras "Program Manager" (por ejemplo, Administrador de programas, tecnologías avanzadas) se muestran en la cuadrícula de datos HTML.  
  
## <a name="preparing-and-sending-the-query"></a>Preparar y enviar la consulta  
 La última parte del subprocedimiento Find_OnClick está formada por dos instrucciones. La primera instrucción asigna el [SQL](../../../ado/reference/rds-api/sql-property.md) propiedad de la [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto igual a la consulta SQL generada de forma dinámica. La segunda instrucción hace que el **RDS. DataControl** objeto (`DC1`) para consultar la base de datos y, a continuación, muestre los nuevos resultados de la consulta en la cuadrícula.  
  
```  
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>Botón Actualizar perfil  
 Al hacer clic en el **Actualizar perfil** botón activa el procedimiento Sub Update_OnClick de VBScript, que ejecuta el [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) del objeto (`DC1`) [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) y [actualizar](../../../ado/reference/rds-api/refresh-method-rds.md) métodos.  
  
```  
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 Cuando `DC1.SubmitChanges` se ejecuta, el servicio de datos remoto empaqueta toda la información de actualización y lo envía al servidor a través de HTTP. La actualización es todo o nada; Si una parte de la actualización es correcta, ninguno de los cambios se realiza y se devuelve un mensaje de estado. `DC1.Refresh`no es necesario después de **SubmitChanges** con servicio de datos remoto, pero garantiza datos actualizados.  
  
## <a name="cancel-changes-button"></a>Botón Cancelar cambios  
 Haga clic en **cancelar cambios** activa el subprocedimiento Cancel_OnClick de VBScript, que ejecuta el [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) del objeto (`DC1)` [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) método.  
  
```  
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 Cuando `DC1.CancelUpdate` se ejecuta, descarta cualquier modificación que haya realizado un usuario en un registro de empleado en la cuadrícula de datos desde la última consulta o actualización. Restaura los valores originales.  
  
## <a name="see-also"></a>Vea también  
 [Botones de navegación de la libreta de direcciones](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)   
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)


