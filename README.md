package com.example.l2ol3otic2.brcallt1;

import android.content.Context;
import android.content.Intent;
import android.support.v7.app.ActionBarActivity;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;


public class MainActivity extends ActionBarActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
    public void broadcastIntent(View view){
        EditText ed1 = (EditText)findViewById(R.id.ed1);
        EditText ed2 = (EditText)findViewById(R.id.ed2);
        String Ans = ed1.getText().toString();
        String Rej = ed2.getText().toString();
        /*Intent intent = new Intent();
        intent.putExtra("answer", Ans);
        intent.putExtra("reject", Rej);
        intent.setAction("com.tutorialspoint.CUSTOM_INTENT");
        sendBroadcast(intent);*/
        Intent x = new Intent(MainActivity.this,CallReceiver.class);
        x.putExtra("answer", Ans);
        x.putExtra("reject", Rej);
        sendBroadcast(x);
    }


    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        // Inflate the menu; this adds items to the action bar if it is present.
        getMenuInflater().inflate(R.menu.menu_main, menu);
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        // Handle action bar item clicks here. The action bar will
        // automatically handle clicks on the Home/Up button, so long
        // as you specify a parent activity in AndroidManifest.xml.
        int id = item.getItemId();

        //noinspection SimplifiableIfStatement
        if (id == R.id.action_settings) {
            return true;
        }

        return super.onOptionsItemSelected(item);
    }
}
