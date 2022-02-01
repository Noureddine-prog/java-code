# java-code

212121simple Notification



final Context context = getApplicationContext();


NotificationManager notificationManager = (NotificationManager) context.getSystemService(Context.NOTIFICATION_SERVICE);

Intent intent = new Intent(MainActivity.this, MainActivity.class); 
intent.setFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP | Intent.FLAG_ACTIVITY_SINGLE_TOP); 
PendingIntent pendingIntent = PendingIntent.getActivity(MainActivity.this, 0, intent, 0); 
androidx.core.app.NotificationCompat.Builder builder; 

    int notificationId = 1;
    String channelId = "channel-01";
    String channelName = "Permissions and Libraries";
    int importance = NotificationManager.IMPORTANCE_HIGH;

    if (android.os.Build.VERSION.SDK_INT >= android.os.Build.VERSION_CODES.O) {
        NotificationChannel mChannel = new NotificationChannel(
                channelId, channelName, importance);
        notificationManager.createNotificationChannel(mChannel);
    }

 
 androidx.core.app.NotificationCompat.Builder mBuilder = new androidx.core.app.NotificationCompat.Builder(context, channelId)
            .setSmallIcon(R.drawable.icon)
            .setContentTitle("Simple Notification")
            .setContentText("Developed by Manish Nirmal")
            .setAutoCancel(true)
            .setOngoing(false)
            .setContentIntent(pendingIntent);
    TaskStackBuilder stackBuilder = TaskStackBuilder.create(context);
    stackBuilder.addNextIntent(intent);
    PendingIntent resultPendingIntent = stackBuilder.getPendingIntent(
            0,
            PendingIntent.FLAG_UPDATE_CURRENT
    );
    mBuilder.setContentIntent(resultPendingIntent);

    notificationManager.notify(notificationId, mBuilder.build());
 
