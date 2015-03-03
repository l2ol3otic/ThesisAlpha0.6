package com.example.l2ol3otic2.brcallt1;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.telephony.TelephonyManager;
import android.view.KeyEvent;
import android.widget.Toast;

public class CallReceiver extends BroadcastReceiver {
    public String cr1,cr2,cx1,cx2;
    @Override
    public void onReceive(Context context, Intent intent) {
            cr1 = intent.getStringExtra("answer");
            cr2 = intent.getStringExtra("reject");
        String text = "Intent Detected.";
        String state = intent.getStringExtra(TelephonyManager.EXTRA_STATE);
        Toast.makeText(context, text+"\n"+"cr1 "+cr1+"\n"+"cx1 "+cx1+"\n"+state, Toast.LENGTH_LONG).show();
        //Toast.makeText(context, text, Toast.LENGTH_LONG).show();
        if (!TelephonyManager.EXTRA_STATE_RINGING.equals(state)){
            cx1=cr1;
            cx2=cr2;
        Toast.makeText(context, text+"\n"+"cr1 "+cr1+"\n"+"cx1 "+cx1+"\n"+state, Toast.LENGTH_LONG).show();
        }
        else if (TelephonyManager.EXTRA_STATE_RINGING.equals(state)) {
            MainActivity a1 = new MainActivity();
            cx1 = a1.Ans;
            cx2 = a1.Rej;
            String incomingNumber = intent.getStringExtra(TelephonyManager.EXTRA_INCOMING_NUMBER);
            Toast.makeText(context,cx1+ "  Incoming" , Toast.LENGTH_LONG).show();
            Toast.makeText(context,incomingNumber , Toast.LENGTH_LONG).show();
            if (incomingNumber.equals(cx1)) {
                Intent i = new Intent(Intent.ACTION_MEDIA_BUTTON);
                i.putExtra(Intent.EXTRA_KEY_EVENT, new KeyEvent(
                        KeyEvent.ACTION_UP, KeyEvent.KEYCODE_HEADSETHOOK));
                context.sendOrderedBroadcast(i, null);
            }
            else {
                Toast.makeText(context,"Reject", Toast.LENGTH_LONG).show();
                Intent i = new Intent(Intent.ACTION_MEDIA_BUTTON);
                i.putExtra(Intent.EXTRA_KEY_EVENT, new KeyEvent(
                        KeyEvent.ACTION_DOWN, KeyEvent.KEYCODE_HEADSETHOOK));
                context.sendOrderedBroadcast(i,"android.permission.CALL_PRIVILEGED");
            }
        }

    }
}

