public string SentMailCHRApprove(data_mas_repair email, string link_system)
        {
            var emailBodies = new List<string>();

            var groupedData = email.data_mas_repair_test_email.GroupBy(item => item.u0_code);
              



            foreach (var group in groupedData)

            {
                
                var body = "<h4>เรียน ผู้เกี่ยวข้องทุกท่าน</h4><br />" +
                           "<strong>รหัสเอกสาร: </strong>" + email.data_mas_repair_test_email[0].u0_code + "<br />" +
                           "<strong>ประเภทการแจ้ง: </strong>" + email.data_mas_repair_test_email[0].typename + "<br />" +
                           "<strong>วันที่สร้างรายการ: </strong>" + email.data_mas_repair_test_email[0].create_date + "<br />" +
                           "<strong>ประเภทการแจ้ง: </strong>" + email.data_mas_repair_test_email[0].remark + "<br />" +
                           "<strong>รหัสพนักงาน: </strong>" + email.data_mas_repair_test_email[0].emp_code + "<br />" +
                           "<strong>ชื่อผู้ทำรายการ: </strong>" + email.data_mas_repair_test_email[0].emp_name_th + "<br />" +
                           "<strong>องค์กร: </strong>" + email.data_mas_repair_test_email[0].org_name_th + "<br />" +
                           "<strong>กลุ่มงาน: </strong>" + email.data_mas_repair_test_email[0].wg_name_th + "<br />" +
                           "<strong>สายงาน: </strong>" + email.data_mas_repair_test_email[0].lw_name_th + "<br />" +
                           "<strong>ฝ่าย: </strong>" + email.data_mas_repair_test_email[0].cen_dept_name_th + "<br />" +
                           "<strong>แผนก: </strong>" + email.data_mas_repair_test_email[0].cen_sec_name_th + "<br />" +
                           "<table border='1' id='dynamic-'>" +
                           "<tr>" +
                           "<th>#</th>" +
                           "<th>ข้อมูลเมนู</th>" +
                           "<th>ข้อมูลพนักงาน</th>" +
                           "</tr>";

                int startNumber = 1;
                foreach (var mas in group)
                {
                    string tableRow = "<tr>" +
                        "<td>" + startNumber + "</td>" +
                        "<td>" + mas.menulv2 + " / " + mas.menulv1 + "</td>" +
                        "<td>" + mas.full_name + "</td>" +
                        "</tr>";

                    body += tableRow;
                    startNumber++;
                }

                body += "</table>" +
                        "<br />" +
                        "<strong>สถานะตำเนินการ: </strong>" + email.data_mas_repair_test_email[0].decision + "<br />" +
                        "<strong>ผู้ดำเนินการ: </strong>" + email.data_mas_repair_test_email[0].emp_name_th + "<br />" +
                        "<strong>ความคิดเห็น : </strong>" + email.data_mas_repair_test_email[0].l0_comment + "<br />" +
                        "<strong>Link: </strong><a href='" + link_system + "'>ระบบ Change Request</a><br />" +
                        "<br />" +
                        "<span style=\"color: red;\"><strong>**สถานะเอกสาร ณ ปัจจุบัน: </strong> " + "ตำเนินการ " + email.data_mas_repair_test_email[0].typename + " โดย " + email.data_mas_repair_test_email[0].act_name + "</span><br />";

                emailBodies.Add(body);
            }

            return string.Join("\n\n", emailBodies);
        }
