# parcial_base_datos

PREGUNTA 21 CREAR UN CURSOR QUE PERMITA MOSTRAR

RESPUESTA

DECLARE @costo_mantenimiento int
DECLARE @haber int

DECLARE db_cursor CURSOR FOR 
select HABER_BAS_INQ from Comercial.INQUILINO

OPEN db_cursor  
FETCH NEXT FROM db_cursor INTO @costo_mantenimiento 

WHILE @@FETCH_STATUS = 0  
BEGIN  
	IF(@costo_mantenimiento < 1500)
		set @costo_mantenimiento = @costo_mantenimiento * 0.075;
	IF(@costo_mantenimiento >= 1500 and @costo_mantenimiento < 2500)
		set @costo_mantenimiento = @costo_mantenimiento * 0.10;
	ELSE 
		set @costo_mantenimiento = @costo_mantenimiento * 0.125;
	  select COD_USUA, NOM_AVAL_INQ, APELL_AVAL, EST_CIVIL_INQ, HABER_BAS_INQ, @costo_mantenimiento as COSTO_MANTENIMIENTO from Comercial.INQUILINO

      FETCH NEXT FROM db_cursor INTO @costo_mantenimiento 
END
CLOSE db_cursor  
DEALLOCATE db_cursor
go
