void change_parameters(int *cmd)
{
    if(start_go_sleep_alarm())
      {
          msg = ACK_R;
          send_msg(&msg);
          state = WAIT;
      }
    else
      {
          if (PAR_IMG())
          { 
            while(PAR_IMG())
                {
                    start_go_sleep_alarm()
                }
            msg = ACK_R;
            send_msg(&msg);
            state = SLEEP;
          }
          else
           { 
            state = SLEEP;
            start_wake_up_alarm();
           }
      }
}

void mod_wait()
{
    if(start_go_sleep_alarm())
      {
          msg = ACK_R;
          send_msg(&msg);
          state = WAIT;
      }
    else
      {
          state = SLEEP;
          start_wake_up_alarm();
      }
}
  

case RECV1:
        //Recebimentos de dados da Esta��o Base. Esse estado deve ficar ativo enquanto houver dados vindo da Esta��o Base.
        //N�o havendo mais dados, deve-se ir para o estado WAIT1 ou para o estado SLEEP.
        //Nota: SET_COMMUNICATION, SEND_TELEMETRY e SEND_PAYLOAD n�o s�o comandos que devem ser processados em RECV1.
            switch(cmd){
                case CHANGE_PAR:
                    change_parameters(&cmd);
                                     
                case GO_SLEEP:
                    state = SLEEP;
                
                default:
                    mod_wait()
            }
            break;
