# Readme
Android >>>working with Timepicker and Datepicker Dialog ,setting Default values with selected value 
.
.
.
.
package com.example.myapplication;

import androidx.appcompat.app.AppCompatActivity;

import android.app.AlertDialog;
import android.app.DatePickerDialog;
import android.app.TimePickerDialog;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.DatePicker;
import android.widget.TextView;
import android.widget.TimePicker;

import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.SimpleTimeZone;

public class MainActivity extends AppCompatActivity {
    Button b1;
    TextView tv;
    int ii, ii1;
    int iii,iii1,iiii2;
    Button b2;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        b1 = (Button) findViewById(R.id.b1);
        b2=(Button)findViewById(R.id.b2);
        tv = (TextView) findViewById(R.id.tv);
        b1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(final View view) {
                Calendar mcurrentTime = Calendar.getInstance();
                int hour = mcurrentTime.get(Calendar.HOUR);
                int minute = mcurrentTime.get(Calendar.MINUTE);
                final TimePickerDialog timePickerDialog;

                timePickerDialog = new TimePickerDialog(MainActivity.this, new TimePickerDialog.OnTimeSetListener() {

                    @Override
                    public void onTimeSet(TimePicker timePicker, int i, int i1) {


                        String format;
                        if (i == 0) {

                            i += 12;

                            format = "AM";
                        } else if (i == 12) {

                            format = "PM";

                        } else if (i > 12) {

                            i -= 12;

                            format = "PM";

                        } else {

                            format = "AM";

                        }
                        tv.setText("current time" + i + ":" + i1 + format);
                        ii = i;
                        ii1 = i1;


                    }
                }, hour, minute, false);
                timePickerDialog.updateTime(ii, ii1);
                timePickerDialog.show();


            }
        });b2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Calendar mcurrentTime = Calendar.getInstance();

                int hour = mcurrentTime.get(Calendar.DAY_OF_MONTH);
                int minute = mcurrentTime.get(Calendar.MONTH);
                final DatePickerDialog datePickerDialog;
                datePickerDialog=new DatePickerDialog(MainActivity.this,DatePickerDialog.THEME_DEVICE_DEFAULT_LIGHT,new DatePickerDialog.OnDateSetListener() {


                    @Override
                    public void onDateSet(DatePicker datePicker, int i, int i1, int i2) {
                        tv.setText("current date"+i+":"+(i1+1)+":"+i2);
                        iii=i;
                        iii1=+i1;
                        iiii2=i2;
                    }
                },hour,minute,1);
                datePickerDialog.show();
                datePickerDialog.updateDate(iii,iii1,iiii2);

            }
        });

    }
}

