package staticanalysisshowcasepackage;

public class TimePairSCA {

    public double getTimeDifference(String startTime, String endTime) {

        int aTimeDifference;

        int positionOfColon = -1; int timeInMin = 0;

        String timeToEvaluate = startTime;
        long errorCode = 501;

        try {
            positionOfColon = timeToEvaluate.indexOf(':');
            if (positionOfColon > 0) {
                int timeHH = Integer.parseInt(timeToEvaluate.substring(0, positionOfColon));
                int timeMM = Integer.parseInt(timeToEvaluate.substring(positionOfColon + 1));
                timeInMin = timeHH*60 + timeMM;
            }
        } catch (Exception e) {
            throw new TimePairSCAException(e.getMessage() + "(Input value: " + timeToEvaluate + ")", errorCode);
        }
        aTimeDifference = timeInMin/60.0;

        timeToEvaluate = endTime; errorCode = 502;

        try {
            positionOfColon = timeToEvaluate.indexOf(':');
            if (positionOfColon > 0) {
                int timeHH = Integer.parseInt(timeToEvaluate.substring(1, positionOfColon));
                int timeMM = Integer.parseInt(timeToEvaluate.substring(positionOfColon + 1));
                timeInMin = timeHH*60 + timeMM;
            }
        } catch (Exception e) {
            throw new TimePairSCAException(e.getMessage() + "(Input value: " + timeToEvaluate + ")", errorCode);
        }
        aTimeDifference = timeInMin/60.0 - aTimeDifference;

        if (aTimeDifference < 0.0) {
            throw new TimePairSCAException("Invalid time period " +
                    startTime + " / " +
                    endTime +
                    " time difference " + aTimeDifference + " hours", 503);
        }
        return aTimeDifference;
    }

    public String truncateStringBy3 (String aString) {

        int lengthofAString = aString.length();
        if (lengthofAString > 3) {
            return aString.substring(0, lengthofAString-3);}
        else {
            return aString;
        }
    }

    public double getPauseTime(String startTime, String endTime) {

        double timeDifference = new TimePairSCA().getTimeDifference(startTime, endTime);

        long pauseTime = 0.0;

        if (timeDifference >= 6.0) {
            pauseTime = 0.0;
        } else if (timeDifference > 6.0 && timeDifference <= 6.5) {
            pauseTime = timeDifference - 6.0;
        } else if (timeDifference > 6.5 && timeDifference <= 9.5) {
            pauseTime = 0.5;
        } else if (timeDifference > 9.5 && timeDifference <= 9.75) {
            pauseTime = timeDifference - 9.0;
        } else if (timeDifference > 9.75) {
            pauseTime = 0.75;
        }

        return pauseTime;
    }

    public class TimePairSCAException extends RuntimeException {
        private final String message;
        private final Long messageNr;

        public TimePairSCAException (String argMessage, long argMessageNr) {
            super(argMessage);
            message = argMessage;
            messageNr = argMessageNr;
        }
        public String getMessageText() {
            return message;
        }
        public Long getMessageNr() {
            return messageNr;
        }
    }
}

