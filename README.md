# java_12_Exception
package ch12_exception;

public class BizException extends Exception {

	private String errCode = "";

	public BizException(String errCode, String errMsg) {
		super(errMsg);
		this.errCode = errCode;
	}

	public BizException(String errMsg) {
		super(errMsg);
	}

	public BizException() {
	}

	public BizException(Exception e) {
		super(e);
	}

	public String getErrCode() {
		return errCode;
	}

}
package ch12_exception;

import java.text.ParseException;

public class ExceptionMain {

	public static void main(String[] args) {
		System.out.println("메인 시작!");
		int[] arr = { 1, 2, 3 };
		String aString = null;
		try {
//			System.out.println(arr[3]);
			aString.length();
		} catch (ArrayIndexOutOfBoundsException e) {
			System.out.println("인덱스문제군!!!");
		} catch (Exception e) {
			System.out.println("문제다!!!");
			e.printStackTrace();
		}
		System.out.println("메인 종료!");

		try {
			ExMethod.printName("");
		} catch (BizException e) {
			System.out.println(e.getErrCode());
			System.out.println(e.getMessage());
			e.printStackTrace();
		}
		
		System.out.println(ExMethod.dateMillsec2("2024/01/18"));
		try {
			System.out.println(ExMethod.dataMillSec("20240118"));
		} catch (ParseException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		System.out.println("종료");
		
		

	}

}
package ch12_exception;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class ExMethod {
	public static void printName(String nm) throws BizException {
		//코드상 오류는 아니지만 해당 없무에서는 오류로 보는 상황에 대한 예외처리방법
		if(nm.length() == 0) {
			throw new BizException("001", "이름에 empty가 들어옴!");
		}else if(nm.length() == 1) {
			throw new BizException("002","외자는 안됨!!");
		}
	}
	public static long dataMillSec(String date) throws ParseException {
		SimpleDateFormat sdf = new SimpleDateFormat("yyyy.MM.dd");
		Date temp = sdf.parse(date);
		return temp.getTime();
	}
	public static long dateMillsec2(String date) {
		SimpleDateFormat sdf = new SimpleDateFormat("yyyy.MM.dd");
		Date temp;
		Long result = 0l;
		try {
			 temp = sdf.parse(date);
			 result = temp.getTime();
		} catch (ParseException e) {
			e.printStackTrace();
		} 
		return result;
	
	}

}
