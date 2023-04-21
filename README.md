# Hello_word
//CONTADOR HORA A HORA

//**********************************************************************
//selecao de hora
IF Minuto >= set_Min_Turnos THEN;
		H:=Hora;
END_IF;
IF Minuto < set_Min_Turnos THEN;
		H:=Hora-1;
END_IF;

//seta valor na hora
C_HH[H]:=Total_hora_atual;

IF H <> monitor_hora THEN;
		Total_hora_atual:=0;
		C_HH[H+1]:=0;
		IF H = 23 THEN;
			C_HH[0]:=0;
		END_IF;
		monitor_hora:=H;
END_IF;
//**********************************************************************

//EXECUÇÃO A CADA PULSO CONTADOR
//Total turno 1
FOR i:=set_Hora_inicioT1 TO set_Hora_inicioT2 DO;
	cnt_geral:=cnt_geral + C_HH[i];
END_FOR;
Total_turno1:=cnt_geral;
cnt_geral:=0;

//Total turno 2
FOR i:=set_Hora_inicioT2 TO set_Hora_inicioT3 DO;
	cnt_geral:=cnt_geral + C_HH[i];
END_FOR;
Total_turno2:=cnt_geral;
cnt_geral:=0;

//Total turno 3
FOR i:=set_Hora_inicioT3 TO set_Hora_inicioT1 DO;
	cnt_geral:=cnt_geral + C_HH[i];
END_FOR;
Total_turno3:=cnt_geral;
cnt_geral:=0;

Total_prod:= Total_turno1 + Total_turno2 + Total_turno3;
//**********************************************************************

//EXECUTA A CADA PULSO NO BOTAO DA IHM ZERA CONTADOR
//ZERA CONTADOR
FOR i :=0 TO 23 DO;
	C_HH[i]:=0;
END_FOR;
Total_hora_atual:=0;
Total_prod:=0;
Total_turno1:=0;
Total_turno2:=0;
Total_turno3:=0;
