# JavaPOC

#changes to have new log for each run
# Log ERROR logs of skipped records to file
log4j.appender.fileLog=com.util.NewLogFileForEachRun
log4j.appender.fileLog.append=true
log4j.appender.fileLog.ImmediateFlush=true
log4j.appender.fileLog.file=/logs/logFile.%RunTime.log
log4j.appender.fileLog.layout=org.apache.log4j.PatternLayout
log4j.appender.fileLog.layout.ConversionPattern=%d{ISO8601} %5p %c{1}:%L - %m%n
log4j.category.fileLog=ERROR, fileLog
log4j.additivity.fileLog=false


import java.text.SimpleDateFormat;
import java.util.Date;

import org.apache.log4j.FileAppender;

/**
 * This class will create new log file for each run
 * 
 * @author: pratibha
 * 
 * @since Aug 6, 2015
 * 
 */
public class NewLogFileForEachRun extends FileAppender {

    @Override
    public void setFile(String fileName) {
        if (fileName.indexOf("%RunTime") >= 0) {
            SimpleDateFormat format = new SimpleDateFormat("yyyyMMddHHmmss");
            fileName = fileName.replaceAll("%RunTime", format.format(new Date()));
        }
        super.setFile(fileName);
    }
}
