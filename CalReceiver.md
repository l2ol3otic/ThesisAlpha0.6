# ThesisAlpha0.6
package com.example.l2ol3otic2.brcallt1;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.telephony.TelephonyManager;
import android.view.KeyEvent;
import android.widget.Toast;

public class CallReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        String cr1 = intent.getStringExtra("answer");
        String cr2 = intent.getStringExtra("reject");
        String text = "Intent Detected.";
        String state = intent.getStringExtra(TelephonyManager.EXTRA_STATE);
        Toast.makeText(context, text+"\n"+"AutoAnswer"+cr1+"\n"+"AutoReject"+cr2+"\n"+state, Toast.LENGTH_LONG).show();
        if (state.equals(TelephonyManager.EXTRA_STATE_RINGING)) {
            String incomingNumber = intent
                    .getStringExtra(TelephonyManager.EXTRA_INCOMING_NUMBER);
            Toast.makeText(context," Incoming" , Toast.LENGTH_LONG).show();
            if (incomingNumber.equals(cr1)) {
                Intent i = new Intent(Intent.ACTION_MEDIA_BUTTON);
                i.putExtra(Intent.EXTRA_KEY_EVENT, new KeyEvent(
                        KeyEvent.ACTION_UP, KeyEvent.KEYCODE_HEADSETHOOK));
                context.sendOrderedBroadcast(i, null);
            }
            else if(incomingNumber.equals(cr2)){
                Intent a = new Intent(Intent.ACTION_MEDIA_BUTTON);
                a.putExtra(Intent.EXTRA_KEY_EVENT, new KeyEvent(
                        KeyEvent.ACTION_DOWN, KeyEvent.KEYCODE_HEADSETHOOK));
                context.sendOrderedBroadcast(a, null);
            }
        }
        else{
            Toast.makeText(context,"no call", Toast.LENGTH_LONG).show();
        }
    }
}

